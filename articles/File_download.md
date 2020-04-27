# Download file from a website and upload it to Dropbox 

## My very first function in powershell ~

```powershell
function Get-UrlInfo {
        [Cmdletbinding()]
        param(
                [Parameter(Mandatory=$true)]
                [String]$fileName

        )
        $fileContent = Get-Content $fileName
        $fileString = $fileContent.Split("</p>")[1] + "</p>"
        $xmlHeader= [xml]$fileString
        $hrefString = $xmlHeader.p.a.href
        $videoId = ([System.Uri]$hrefString).Query.Split("=")[1]
        $videoUrl = "https://fast.wistia.net/embed/iframe/" + $videoId

        # Download the video from the above URL
        youtube-dl $videoUrl

        # Get the name of the downloaded file
        $outputFile = Get-ChildItem *.bin -Name
        $fileString = $outputFile.Split("-")[0]+"-$videoId" + ".mp4"

        # Rename the downloaded file
        $renameFile = mv $outputFile $fileString

        # Upload the file on to Dropbox
        rclone copy *.mp4 remote:/Videos/ -v
}
```
## This is how the help file looks like

```powershell
PS /root/projects/perl_one_liners/assignment> Get-Help Get-UrlInfo -Detailed

NAME
    Get-UrlInfo
    
SYNTAX
    Get-UrlInfo [-fileName] <string> [[-filePath] <string[]>] [<CommonParameters>]
    
    
PARAMETERS
    -fileName <string>
    
    -filePath <string[]>
    
    <CommonParameters>
        This cmdlet supports the common parameters: Verbose, Debug,
        ErrorAction, ErrorVariable, WarningAction, WarningVariable,
        OutBuffer, PipelineVariable, and OutVariable. For more information, see
        about_CommonParameters (https://go.microsoft.com/fwlink/?LinkID=113216). 
    

ALIASES
    None
```
# Another function using the url string as a parameter

```powershell

function Save-Video {
        [Cmdletbinding()]
        param(
                [Parameter(Mandatory=$true)]
                [String]$urlString
        )
        $videoId = ([System.Uri]$urlString).Query.Split("=")[1]
        $videoUrl = "https://fast.wistia.net/embed/iframe/" + $videoId

        # Download the video from the above URL
        youtube-dl $videoUrl

        # Get the name of the downloaded file
        $outputFile = Get-ChildItem *.bin -Name
        $fileString = $outputFile.Split("-")[0]+"-$videoId" + ".mp4"

        # Rename the downloaded file
        $renameFile = mv $outputFile $fileString

        # Upload the file on to Dropbox
        rclone copy *.mp4 remote:/Videos/ -v
}

PS /root/projects/perl_one_liners/assignment> Save-Video

cmdlet Save-Video at command pipeline position 1
Supply values for the following parameters:
urlString: https://university.business-science.io/courses/541207/lectures/15050206?wvideo=9gj4s6uckw
[Wistia] 9gj4s6uckw: Downloading JSON metadata
[download] Destination: lab_31_google_analytics_prophet.mp4-9gj4s6uckw.bin
[download] 100% of 348.45MiB in 00:12
2020/04/26 09:25:54 INFO  : lab_31_google_analytics_prophet.mp4-9gj4s6uckw.mp4: Copied (new)
2020/04/26 09:25:54 INFO  : 
Transferred:      348.454M / 348.454 MBytes, 100%, 18.835 MBytes/s, ETA 0s
Transferred:            1 / 1, 100%
Elapsed time:        18.4s

PS /root/projects/perl_one_liners/assignment>
```