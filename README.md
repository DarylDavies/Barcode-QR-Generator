# Barcode-QR-Generator
## This webapp Generates, Scans, Reads Barcode and QR code.

Both QR codes and barcodes store information about an item or product in a machine-readable format that can be easily scanned with a barcode scanner or, more recently, many smartphones (when equipped with a barcode-scanning app or QR code reader). Using QR codes is a great way to streamline the user experience and ensure customers can access information as quickly and efficiently as possible. By scanning a QR code, customers can go straight to a landing page or check-in at a location without having to speak to a staff member or ask for support. Nowadays it is widely used in online payment.
## Software
[Visual Studio 2019 ](https://visualstudio.microsoft.com/downloads/)
## Framework
[ASP.NET MVC ](https://dotnet.microsoft.com/en-us/apps/aspnet/mvc)
## Hosting
[Azure Web App Services](https://azure.microsoft.com/en-in/services/app-service/web/)

Azure App Service is an HTTP-based service for hosting web applications, REST APIs, and mobile back ends. You can develop in your favorite language, be it .NET, .NET Core, Java, Ruby, Node.js, PHP, or Python. Applications run and scale with ease on both Windows and Linux-based environments.Azure App Service is a fully managed platform as a service (PaaS) offering for developers.
## Install
[IDAutomationHC39M Free Version Font](https://www.wfonts.com/font/idautomationhc39m-free-version)

``` PM> Install-Package ZXing.Net.Bindings.Windows.Compatibility -Version 0.16.10 ```

``` PM> Install-Package System.Drawing.Common -Version 6.0.0 ```

``` PM> Install-Package QRCoder -Version 1.4.3 ```
## Screenshots
**Barcode Generator**

![image](https://user-images.githubusercontent.com/92319855/151719237-0e29d76a-d4d4-49a2-af37-87e97a158e04.png)

**Barcode Scanner & Reader**

https://user-images.githubusercontent.com/92319855/151722654-733cefa7-752d-420f-ac97-94921c85e194.mp4

**QR code Generator**

![image](https://user-images.githubusercontent.com/92319855/151719449-46ec835d-1186-4dde-a62b-cba3887e40c1.png)

**QR code Reader**

![image](https://user-images.githubusercontent.com/92319855/151719492-82155fdd-7be5-4c41-ade5-8e99d5fe88e0.png)

**QR code Scanner**

https://user-images.githubusercontent.com/92319855/151720347-0d6d582a-8e07-45b3-94dc-65d53b83e58b.mp4

## Code Snippet
**Main code for Barcode**
```//The Image is drawn based on length of Barcode text.
                using (Bitmap bitMap = new Bitmap(barcode.Length * 30, 80))
                {
                    //The Graphics library object is generated for the Image.
                    using (Graphics graphics = Graphics.FromImage(bitMap))
                    {
                        //The installed Barcode font.
                        Font oFont = new Font("IDAutomationHC39M Free Version", 16);
                        PointF point = new PointF(2f, 2f);

                        //White Brush is used to fill the Image with white color.
                        SolidBrush whiteBrush = new SolidBrush(Color.White);
                        graphics.FillRectangle(whiteBrush, 0, 0, bitMap.Width, bitMap.Height);

                        //Black Brush is used to draw the Barcode over the Image.
                        SolidBrush blackBrush = new SolidBrush(Color.Black);
                        graphics.DrawString("*" + barcode + "*", oFont, blackBrush, point);
                    }

                    //The Bitmap is saved to Memory Stream.
                    bitMap.Save(ms, ImageFormat.Png);

                    //The Image is finally converted to Base64 string.
                    ViewBag.BarcodeImage = "data:image/png;base64," + Convert.ToBase64String(ms.ToArray());
                } 
 ```
**Main code for QR code**
```
           {
            var writer = new QRCodeWriter();
            var resultBit = writer.encode(formCollection["QRCodeString"], BarcodeFormat.QR_CODE, 200, 200);
            var matrix = resultBit;
            int scale = 2;
            Bitmap result = new Bitmap(matrix.Width * scale, matrix.Height * scale);
            for (int x = 0; x < matrix.Height; x++)
            {
                for(int y = 0; y < matrix.Width; y++)
                {
                    Color pixel = matrix[x, y] ? Color.Black : Color.White;
                    for (int i = 0; i < scale; i++)
                        for (int j = 0; j < scale; j++)
                            result.SetPixel(x * scale + i, y * scale + j, pixel);
                }
            }
            string webRootPath = _hostEnvironment.WebRootPath;
            result.Save(webRootPath + "\\Image\\QrcodeNew.png");
            ViewBag.URL = "\\Image\\QrcodeNew.png";
            return View();
            }
```


