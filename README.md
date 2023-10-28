# Download Html Source

Download Html Source From A Specific LINK or URL?

+ [Program.cs](https://raw.githubusercontent.com/gtechsltn/aspnet-ebooks/master/ConsoleApp2/Program.cs)

```
// 
// Refer: https://raw.githubusercontent.com/gtechsltn/aspnet-ebooks/master/ConsoleApp2/Program.cs
// 
using System;
using System.Diagnostics;
using System.IO;
using System.Net;
using System.Net.Http;
using System.Text;
using System.Threading.Tasks;

namespace ConsoleApp2
{
    internal class Program
    {
        private static void Main(string[] args)
        {
            MainAsync(args).GetAwaiter().GetResult();
        }

        private static async Task MainAsync(string[] args)
        {
            var stopwatch = new Stopwatch();
            stopwatch.Start();

            string[] urls = new[] {
                    "https://myaccount.google.com/                                                                           ".Trim(),
                    "https://wpmailsmtp.com/gmail-less-secure-apps/                                                          ".Trim(),
                    "https://myaccount.google.com/lesssecureapps                                                             ".Trim(),
                    "https://myaccount.google.com/device-activity                                                            ".Trim(),
                    "https://www.google.com/settings/security/lesssecureapps                                                 ".Trim(),
                    "https://myaccount.google.com/lesssecureapps                                                             ".Trim(),
                    "https://myaccount.google.com/security                                                                   ".Trim(),
                    "https://myaccount.google.com/apppasswords                                                               ".Trim(),
                    "https://support.google.com/mail/answer/185833?hl=vi                                                     ".Trim(),
                    "https://123host.vn/tailieu/kb/hosting/huong-dan-tao-mat-khau-ung-dung-cho-gmail.html                    ".Trim(),
                    "https://fptshop.com.vn/tin-tuc/thu-thuat/cach-tao-mat-khau-ung-dung-gmail-146054                        ".Trim(),
                    "https://www.7host.vn/huong-dan-lay-mat-khau-ung-dung-mail-tren-tai-khoan-google-gmail/                  ".Trim(),
                    "https://help.tenten.vn/huong-dan-tao-mat-khau-ung-dung-cho-gmail/                                       ".Trim(),
                    "https://www.jotform.com/help/392-how-to-use-your-gmail-account-as-your-email-sender-via-smtp/           ".Trim(),
                    "https://learn.microsoft.com/en-us/answers/questions/1167393/send-email-form-gmail-account-using-c       ".Trim(),
                    "https://docs.google.com/document/d/1edGFF-y82P4IYHsEixsuMd1DB2qUxy8OCsm0wwQ0J24/                        ".Trim(),
                    "https://www.aspsnippets.com/Articles/GMAIL-SMTP-Error-Failure-sending-email.aspx                        ".Trim(),
                    "https://www.youtube.com/watch?v=TmInjjA0cNc                                                             ".Trim(),
                    "https://stackoverflow.com/questions/57644814/c-sharp-sending-email-via-gmail-account                    ".Trim(),
                    "https://stackoverflow.com/questions/29465096/how-to-send-an-e-mail-with-c-sharp-through-gmail           ".Trim(),
                    "https://www.courier.com/guides/csharp-send-email/                                                       ".Trim(),
                    "https://stackoverflow.com/questions/32260/sending-email-in-net-through-gmail                            "
                };
            var realPath = string.Empty;
            var htmlSource = string.Empty;
            foreach (var url in urls)
            {
                try
                {
                    var tempUrl = url.Replace("://", "_")
                        .Replace("/", "_")
                        .Replace("?", "")
                        .Replace("&", "")
                        .Replace("=", "")
                        .Replace("html", "")
                        .Replace("htm", "");
                    realPath = $@"D:\Pages\{tempUrl}.html";
                    string realFolder = Path.GetDirectoryName(realPath);
                    if (!Directory.Exists(realFolder))
                    {
                        Directory.CreateDirectory(realFolder);
                    }
                    using (WebClient wc = new WebClient())
                    {
                        htmlSource = wc.DownloadString(url);
                        if (!string.IsNullOrWhiteSpace(htmlSource))
                        {
                            File.WriteAllText(realPath, htmlSource, Encoding.UTF8);
                        }
                    }
                }
                catch (Exception ex)
                {
                    Debug.WriteLine(ex);
                    //throw;

                    using (HttpClient client = new HttpClient())
                    {
                        using (HttpResponseMessage response = await client.GetAsync(url))
                        {
                            using (HttpContent content = response.Content)
                            {
                                htmlSource = await content.ReadAsStringAsync();
                                if (!string.IsNullOrWhiteSpace(htmlSource))
                                {
                                    File.WriteAllText(realPath, htmlSource, Encoding.UTF8);
                                }
                            }
                        }
                    }
                }
            }
            stopwatch.Stop();
            Console.WriteLine("Elapsed: {0} ms", stopwatch.ElapsedMilliseconds);
            Console.Write("DONE. Press any key to exit...");
            Console.ReadKey();
        }
    }
}
```
