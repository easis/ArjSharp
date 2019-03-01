# ArjSharp
A quick and (very) dirty implementation of ARJ archive in C#.

# References
* https://github.com/chapgaga/farmanager/blob/41d51b92b32ea48bb3586fae0ebb5718e9ff984f/plugins/multiarc/arj.cpp
* http://geos.icc.ru:8080/scripts/WWWBinV.dll/ShowR?ARJ.rfh
                
# Example
```csharp
public static void CreateFile(string outputName, string filename, string output)
{
  ArjMainHeader mainHeader = new ArjMainHeader(Path.GetFileName(outputName));

  List<byte> fileData = new List<byte>();
  fileData.AddRange(mainHeader.GetBytes());

  FileInfo f = new FileInfo(filename);
  ArjMainFileHeader fileHeader = new ArjMainFileHeader(f, output);

  fileData.AddRange(fileHeader.GetBytes());

  File.WriteAllBytes(outputName, fileData.ToArray());
}

static void Main(string[] args)
{
  CreateFile("test.arj", @"test.txt", @"test/test.txt");
  //CreateFile("test.arj", @"test.txt", @"C:\C:C:../../AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup\test.txt"); does not work :)
}
```
