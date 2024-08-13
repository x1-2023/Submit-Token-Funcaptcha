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
