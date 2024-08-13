# Submit-Token-Funcaptcha
How to submit bypass token to HOTMAIL/OUTLOOK captcha?

## Run the browser with arguments 
```
--disable-web-security
--disable-site-isolation-trials
--disable-application-cache
```

#Get Token from any service (2captcha, dortcap...)

#Execute javascript below:
```
var captchaToken = 'INPUT_TOKEN_HERE';
var enc = document.getElementById('enforcementFrame');
var encWin = enc.contentWindow || enc;
var encDoc = enc.contentDocument || encWin.document;
let script = encDoc.createElement('SCRIPT');
script.append('function CaptchaSubmit(token) { parent.postMessage(JSON.stringify({ eventId: "challenge-complete", payload: { sessionToken: token } }), "*") }');
encDoc.documentElement.appendChild(script);
encWin.CaptchaSubmit(captchaToken);
```
--------------------------------------------------

```
var anyCaptchaToken = [[TOKEN]];

// Tạo một hàm để gửi token
function sendToken(token) {
    window.postMessage(JSON.stringify({
        eventId: "challenge-complete",
        payload: { sessionToken: token }
    }), "*");
}

// Kiểm tra xem iframe đã tải chưa
function checkIframeAndSendToken() {
    var arkoseFrame = document.getElementById('arkoseFrame');
    if (arkoseFrame) {
        // Gửi token qua postMessage
        sendToken(anyCaptchaToken);
    } else {
        // Nếu iframe chưa tải, thử lại sau 100ms
        setTimeout(checkIframeAndSendToken, 100);
    }
}

// Bắt đầu quá trình kiểm tra và gửi token
checkIframeAndSendToken();

// Lắng nghe phản hồi từ iframe (nếu cần)
window.addEventListener('message', function(event) {
    // Kiểm tra nguồn gốc của tin nhắn nếu cần
    // if (event.origin !== "https://expected-origin.com") return;
    
    try {
        var data = JSON.parse(event.data);
        if (data.eventId === "captcha-response") {
            console.log("Captcha response received:", data.payload);
            // Xử lý phản hồi ở đây
        }
    } catch (error) {
        console.error("Error parsing message:", error);
    }
}, false);
```


- Cách gửi mã thông báo Funcaptcha Token
- Đầu tiên, bạn phải tập trung vào iframe có id "arkoseFrame"

- Với Code Selenium

- Chuyển iframe bằng Code C#:
```
driver.SwitchTo().Frame(driver.FindElement(By.Id("arkoseFrame")));
```

- Chuyển iframe bằng Code Python:
```
driver.switch_to.frame(driver.find_element(By.ID, 'arkoseFrame'));
```

- Chuyển iframe bằng Code Java:
```
WebElement iframe = driver.findElement(By.id("arkoseFrame"));
```

- Switch to the frame
```
driver.switchTo().frame(iframe);
```

- Submit Fun Token:
```
var Token_FunCaptCha = "Truyền token nhận đc từ api vào đây - xem ví dụ phía dưới";
var Js_Submit = @"
function submit(token) {
    parent.postMessage(JSON.stringify({
        eventId: 'challenge-complete',
        payload: { sessionToken: token }
    }), '*');
}
submit('"+Token_FunCaptCha+"');
";

driver.execute_script(Js_Submit); // inject javascripts code submit token vào trình duyệt trong selenium
```

- Với Token_FunCaptCha là Code thông báo Funcaptcha bạn nhận được từ dịch vụ [CaptCha69.Com](https://captcha69.com/)
- Token_FunCaptCha có dạng:
```
12017d5cd8966fb68.4052468405|r=eu-west-1|meta=3|meta_width=558|meta_height=523|metabgclr=transparent|metaiconclr=%23555555|guitextcolor=%23000000|lang=vi|pk=2CB16598-CB82-4CF7-B332-5990DB66F3AB|at=40|ag=101|cdn_url=https%3A%2F%2Fclient-api.arkoselabs.com%2Fcdn%2Ffc|lurl=https%3A%2F%2Faudio-eu-west-1.arkoselabs.com|surl=https%3A%2F%2Fclient-api.arkoselabs.com|smurl=https%3A%2F%2Fclient-api.arkoselabs.com%2Fcdn%2Ffc%2Fassets%2Fstyle-manager
```







