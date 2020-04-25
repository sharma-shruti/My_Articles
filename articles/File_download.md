# Download file from a website and upload it to Dropbox 

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
        $key = ([System.Uri]$hrefString).Query.Split("=")[1]
        $url = "https://fast.wistia.net/embed/iframe/" + $key

        # Download the video from the above URL
        youtube-dl $url

        # Get the name of the downloaded file
        $outputFile = Get-ChildItem *.bin -Name
        $fileString = $outputFile.Split("-")[0]+"-$key" + ".mp4"

        # Rename the downloaded file
        $renameFile = mv $outputFile $fileString

        # Upload the file on to Dropbox
        rclone copy *.mp4 remote:/Videos/ -v
}
```