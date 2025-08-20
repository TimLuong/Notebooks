// Configuration object for AI models/endpoints
const AI_MODELS_CONFIG = {
  kinkin4o: {
    apiKey: "3cc727883d7d4dfd8720f47fdd0bca61",
    endpoint: "https://kinkin.openai.azure.com/openai/deployments/KinKin4o/chat/completions?api-version=2024-02-15-preview"
  },
  gpt4o: { // Example: configuration for the model used in the original aiPrompt
    apiKey: "c85e3aee87b3438592ba00ada7565115",
    endpoint: "https://tintinaiservices.openai.azure.com/openai/deployments/gpt-4o/chat/completions?api-version=2024-02-15-preview"
  }
  // Add other models here as needed
};

// --- System Role Definitions ---
const SYSTEM_ROLE_TEAM_MANAGER_D365_SUPPORT = "You are Cong.Luong-Minh (Cong.luong-minh@tek-experts.com) a Team Manager who manages a team of Dynamics 365 Customer Services and Support.\nWhen reviewing email conversations of your team members, it is sufficient to refer to individuals using their first names, including yourself.";
const SYSTEM_ROLE_TEAM_MANAGER_D365_FINOPS_APAC = "You are Cong.Luong-Minh (Cong.luong-minh@tek-experts.com), a Team Manager responsible for overseeing a customer support team specializing in Dynamics 365 Finance and Operations within the APAC Region. Your role includes managing and guiding the team to deliver exceptional customer service across various technical service lines. When reviewing email conversations of your team members, it is sufficient to refer to individuals using their first names, including yourself.";

// --- Prompt Instruction Definitions ---
const PROMPT_INSTRUCTION_SUMMARIZE_EMAIL = "Analyse email conversation below and summarize the email thread as detail as possible, using tabs and bullets format if needed, consider listing events and linking event by timeline with timestamp in format 'yyyy.mm.dd hh:mm'. You have to devide into 3 paragraph following this format: 1. General info: {Summarization from viewpoint of a Team Manager, using indirect speech, without pronouns, short }\n 2. Timeline analysis: {Primary Events timeline with keypoints}\n 3. Action plan: {Conclusion and recommendation next action for you}. The email content is:";
const PROMPT_INSTRUCTION_COACHING_PDP = "Task: Develop a Structured Email Template Titled \"ENGINEER & MANAGER 1:1 on Performance Development Plan\"\r\n\r\nObjective:\r\nCreate a detailed action plan email following a recent 1:1 coaching session on Performance Development Planning (PDP), utilizing the ACE Documentation Form as a reference. Use today's date for the coaching session.\r\n\r\nInstructions:\r\nConversation Type: Coaching\r\n2. Deep Dive Analysis:\r\nAnalyse engineer PDP plan.\r\n\r\n3. Engineer Success Action Plan/Commitment:\r\n\r\nOpportunity: [Identify specific areas where the engineer needs improvement.]\r\nRoot Cause: [Analyze the underlying reasons behind the opportunity, if applicable.]\r\nAction Plan: [Outline specific steps the engineer will take to address the opportunity.]\r\nCommitment: [Confirm the engineer's understanding and commitment to implementing the action plan.]\r\n\r\n4. Manager Success Action Plan:\r\n\r\nAction Plan: [Detail the support the manager will provide to help the engineer achieve their goals. Include resources, training, and ongoing feedback. Use S.M.A.R.T Goals]\r\n5. Follow-up:\r\nFollow-up Date: [Schedule a follow-up coaching session this day next month to track progress and adjust the action plan as needed.]\r\n\r\nAdditional Instructions:\r\nEnsure the template clearly communicates objectives and expectations.\r\nAdd personalized elements by addressing the engineer by name.\r\nInclude thoughtful touches to foster engagement and motivation.\r\nEmail Content from the Engineer for Processing and Analysis:";
const PROMPT_INSTRUCTION_GENERAL_COACHING_ACE = "You have just completed a coaching session with your engineer to address feedback from the QA team regarding a support case. During the session, you discussed the need for improvement in [SE Name]'s [focus area, e.g., case documentation, communication with customers]. You worked together to develop a plan for improvement, including SMART goals and action steps.\r\nNow, use the ACE template provided below to document this coaching session:\r\n1. Coaching Session Overview\r\n* Why: Briefly describe the reason for the coaching session (e.g., address feedback from QA, identify areas for improvement, etc.).\r\n* What: Summarize the key coaching focus areas (e.g., case documentation, communication, etc.).\r\n* When: Specify the date and time of the coaching session.\r\n* How: Describe the approach used in the coaching session (e.g., constructive feedback, coaching, difficult conversation).\r\n2. Session Information\r\nSE Name: [Insert SE Name]\r\nDepartment: Dynamics 365 ERP Customer Services and Support\r\nDate: [Date of Coaching Session]\r\nTime: [Start and End Time of Coaching Session]\r\n3. Deep Dive Analysis\r\nCoaching Focus Area 1: [Insert Focus Area 1]\r\nFocus Area L2: [Insert Focus Area 2]\r\n4. Engineer Success Action Plan / Commitment\r\nCoaching:\r\nOpportunity: [Identify the specific skill or knowledge gap needing improvement]\r\nRoot Cause: [Explore the root cause of the opportunity, e.g., lack of training, lack of practice]\r\nAction Plan: [Outline the action steps the employee will take to improve]\r\nGoal 1: [Insert Goal 1]\r\nS (Specific): [Describe the goal in specific terms]\r\nM (Measurable): [Describe how the goal will be measured]\r\nA (Achievable): [Explain why the goal is achievable]\r\nR (Relevant): [Explain how the goal is relevant to the situation]\r\nT (Time-Bound): [Set a clear timeframe for achieving the goal]\r\nGoal 2: [Insert Goal 2]\r\nS (Specific): [Describe the goal in specific terms]\r\nM (Measurable): [Describe how the goal will be measured]\r\nA (Achievable): [Explain why the goal is achievable]\r\nR (Relevant): [Explain how the goal is relevant to the situation]\r\nT (Time-Bound): [Set a clear timeframe for achieving the goal]\r\nCommitment: [Document the employee's commitment to implementing the action plan and any agreed-upon timelines]\r\n5. Manager Success Action Plan:\r\nAction 1: [Outline the manager's support, e.g., providing resources, reviewing progress, offering guidance]\r\nS (Specific): [Describe the goal in specific terms]\r\nM (Measurable): [Describe how the goal will be measured]\r\nA (Achievable): [Explain why the goal is achievable]\r\nR (Relevant): [Explain how the goal is relevant to the situation]\r\nT (Time-Bound): [Set a clear timeframe for achieving the goal]\r\nAction 2: [Include any additional support or follow-up actions]\r\nS (Specific): [Describe the goal in specific terms]\r\nM (Measurable): [Describe how the goal will be measured]\r\nA (Achievable): [Explain why the goal is achievable]\r\nR (Relevant): [Explain how the goal is relevant to the situation]\r\nT (Time-Bound): [Set a clear timeframe for achieving the goal]\r\n6. Follow-up and Acknowledgement:\r\nFollow-up Date: [Date of Next Review/Meeting]\r\nAcknowledgement: [Document the employee's acknowledgement of the coaching and their commitment to the action plan]\r\nEmail Content from QA team:";
const PROMPT_INSTRUCTION_CUSTOM_REQUEST_BASE = "Do this: ";
const PROMPT_INSTRUCTION_CUSTOM_REQUEST_EMAIL_CONTEXT = "By reading this previous email thread ";

// Gán sự kiện click cho các button trên giao diện HTML
// Khi button với id "submitButton" được click, hàm submitButton sẽ được gọi
$("#submitButton").click(submitButton);
// Khi button với id "emailSummarize" được click, hàm emailSummarize sẽ được gọi
$("#emailSummarize").click(emailSummarize);
// Khi button với id "generalCoaching" được click, hàm generalCoaching sẽ được gọi
$("#generalCoaching").click(generalCoaching);
// Khi button với id "generalCoachingPDP" được click, hàm generalCoachingPDP sẽ được gọi
$("#generalCoachingPDP").click(generalCoachingPDP);

// Khai báo biến toàn cục để lưu trữ output (hiện tại chưa được sử dụng nhiều)
let output = "";

// Hàm emailSummarize: Lấy nội dung email hiện tại, gửi đến AI để tóm tắt và hiển thị kết quả tóm tắt trong một cửa sổ trả lời mới.
function emailSummarize() {
  // Ghi log ra console để theo dõi quá trình hoạt động
  console.log("Stating generate Summarize email. Please wait...");
  // Gọi hàm getOutput để lấy nội dung email đã được xử lý
  getOutput()
    .then((emailBody) => { // Renamed result to emailBody for clarity
      // Gọi hàm aiPrompt4 đã được refactor, sử dụng các hằng số
      aiPrompt4(
        "kinkin4o",                                 // modelIdentifier
        SYSTEM_ROLE_TEAM_MANAGER_D365_SUPPORT,      // systemRoleContent
        PROMPT_INSTRUCTION_SUMMARIZE_EMAIL,         // instructionPrompt
        emailBody                                   // emailBodyContent
      )
        .then((aiGeneratedContent) => { // Renamed result to aiGeneratedContent
          // Ghi log kết quả từ AI
          console.log("Summarize content generated. Poping up in new Reply Window");
          // Chuyển đổi kết quả tóm tắt (plain text) sang định dạng HTML
          let htmlx = plainTextToHtml(aiGeneratedContent);

          // Hiển thị nội dung HTML trong một cửa sổ trả lời email mới (ReplyAll)
          Office.context.mailbox.item.displayReplyAllForm({ htmlBody: htmlx });
        })
        .catch((error) => console.error("Error in emailSummarize AI call:", error));
    })
    .catch((error) => console.error("Error in emailSummarize getOutput:", error));
}

// Hàm generalCoachingPDP: Tạo email huấn luyện (coaching) cho Kế hoạch Phát triển Hiệu suất (PDP).
function generalCoachingPDP() {
  // Ghi log bắt đầu quá trình
  console.log("Stating generate General Coaching PDP email. Please wait...");
  // Lấy nội dung email hiện tại để làm ngữ cảnh
  getOutput()
    .then((emailBody) => {
      // Gọi AI để tạo nội dung email coaching PDP
      aiPrompt4(
        "kinkin4o",                                 // modelIdentifier
        SYSTEM_ROLE_TEAM_MANAGER_D365_FINOPS_APAC,  // systemRoleContent
        PROMPT_INSTRUCTION_COACHING_PDP,            // instructionPrompt
        emailBody                                   // emailBodyContent
      )
        .then((aiGeneratedContent) => {
          // result chứa nội dung email coaching PDP từ AI
          console.log("Coaching PDP content generated. Poping up in new Reply Window");
          // Chuyển đổi sang HTML
          let htmlx = plainTextToHtml(aiGeneratedContent);
          // Hiển thị trong cửa sổ trả lời mới
          Office.context.mailbox.item.displayReplyAllForm({ htmlBody: htmlx });
        })
        .catch((error) => console.error("Error in generalCoachingPDP AI call:", error));
    })
    .catch((error) => console.error("Error in generalCoachingPDP getOutput:", error));
}

// Hàm generalCoaching: Tạo email huấn luyện (coaching) chung.
function generalCoaching() {
  // Ghi log bắt đầu
  console.log("Stating generate General Coaching email. Please wait...");
  // Lấy nội dung email hiện tại
  getOutput()
    .then((emailBody) => {
      // Gọi AI để tạo nội dung email coaching
      aiPrompt4(
        "kinkin4o",                                 // modelIdentifier
        SYSTEM_ROLE_TEAM_MANAGER_D365_FINOPS_APAC,  // systemRoleContent
        PROMPT_INSTRUCTION_GENERAL_COACHING_ACE,    // instructionPrompt
        emailBody                                   // emailBodyContent
      )
        .then((aiGeneratedContent) => {
          // result chứa nội dung email coaching từ AI
          console.log("General Coaching content generated. Poping up in new Reply Window");
          let htmlx = plainTextToHtml(aiGeneratedContent);
          Office.context.mailbox.item.displayReplyAllForm({ htmlBody: htmlx });
        })
        .catch((error) => console.error("Error in generalCoaching AI call:", error));
    })
    .catch((error) => console.error("Error in generalCoaching getOutput:", error));
}

// Hàm submitButton: Xử lý yêu cầu tùy chỉnh từ người dùng nhập vào textArea.
function submitButton() {
  const userCustomInstruction = $("#textArea").val();
  // Ghi log yêu cầu của người dùng và thông báo chờ xử lý
  console.log("Your input is:  " + userCustomInstruction + ". Hold on for Zumei to process your request");
  // Lấy nội dung email hiện tại
  getOutput()
    .then((emailBody) => {
      // Construct the full instruction for custom requests
      const fullInstruction = PROMPT_INSTRUCTION_CUSTOM_REQUEST_BASE + userCustomInstruction + " " + PROMPT_INSTRUCTION_CUSTOM_REQUEST_EMAIL_CONTEXT;
      
      // Gọi AI với yêu cầu tùy chỉnh từ textArea và nội dung email gốc
      aiPrompt4(
        "kinkin4o",                                 // modelIdentifier
        SYSTEM_ROLE_TEAM_MANAGER_D365_SUPPORT,      // systemRoleContent (or choose another appropriate role)
        fullInstruction,                            // instructionPrompt (which now includes user's custom part)
        emailBody                                   // emailBodyContent
      )
        .then((aiGeneratedContent) => {
          // Ghi log chi tiết về prompt đã gửi và kết quả nhận được
          console.log(
            "Custom request content generated. Poping up new Reply Window. History prompt: " + fullInstruction + emailBody
          );
          let htmlx = plainTextToHtml(aiGeneratedContent);
          Office.context.mailbox.item.displayReplyAllForm({ htmlBody: htmlx });
        })
        .catch((error) => console.error("Error in submitButton AI call:", error));
    })
    .catch((error) => console.error("Error in submitButton getOutput:", error));
}

// Hàm getOutput: Lấy và xử lý sơ bộ nội dung của email hiện đang mở trong Outlook.
// Trả về một Promise chứa nội dung email đã được định dạng.
function getOutput() {
  return new Promise((resolve, reject) => {
    // Lấy thông tin người gửi
    const from = Office.context.mailbox.item.from.emailAddress;
    // Lấy thông tin thời gian gửi và định dạng lại
    const sent = new Date(Office.context.mailbox.item.dateTimeCreated).toLocaleString("en-US", {
      weekday: "long",
      month: "long",
      day: "numeric",
      year: "numeric",
      hour: "numeric",
      minute: "numeric",
      timeZoneName: "short"
    });
    // Lấy danh sách người nhận và nối thành chuỗi
    const to = Office.context.mailbox.item.to.map((recipient) => recipient.emailAddress).join(", ");
    // Lấy tiêu đề email
    const subject = Office.context.mailbox.item.subject;
    // Lấy nội dung email dưới dạng văn bản thuần túy (plain text)
    Office.context.mailbox.item.body.getAsync("text", { asyncContext: "This is passed to the callback" }, function(
      result
    ) {
      // Kiểm tra nếu lấy nội dung thành công
      if (result.status === Office.AsyncResultStatus.Succeeded) {
        let body = result.value; // Nội dung email gốc

        // Xóa các URL khỏi nội dung email
        body = body.replace(/https?:\/\/[^\s]+/g, "");

        // Xóa các dòng trống
        body = body.replace(/^\s*[\r\n]/gm, "");

        // Xóa các dòng "Cc:"
        body = body.replace(/Cc:.*\n/g, ""); // Remove all lines that start with "Cc:"
        body = body.replace(/CC:.*\n/g, ""); // Remove all lines that start with "Cc:"
        // Gọi hàm removeKeywords để xóa các từ khóa không cần thiết (thường là chữ ký)
        body = removeKeywords(body, [
          "Regards,",
          "Kind Regards",
          "Kind regards,",
          "Kind regards",
          "Best regards,",
          "Best regards",
          "Thank and best regards,",
          "Support Consultant",
          "HKBN Group",
          "Thank you,",
          "Thanks,",
          "Technical Support Engineer",
          "+61 481 035 570"
        ]);
        // Tạo chuỗi output chứa thông tin email đã định dạng
        output = `From: ${from}\nSent: ${sent}\nTo: ${to}\nSubject: ${subject}\nEmail body: ${body}`;
        var tokens = output.length; // Độ dài của chuỗi output
        var xoutput; // Biến tạm để lưu trữ output đã cắt bớt (nếu cần)
        console.log("Number of words on RAW email extracted:" + tokens);

        // Giới hạn độ dài của output để tránh vượt quá giới hạn token của AI
        if (output.length > 10) { // Kiểm tra này có vẻ không cần thiết vì output luôn dài hơn 10 nếu có nội dung
          console.log("Need to split");
          xoutput = output
            //.split(" ") // Tạm thời comment lại việc split theo từ
            .slice(0, 35000); // Cắt chuỗi nếu quá dài

          //.join(" ") + "..."; // Tạm thời comment lại việc nối lại
        }
        tokens = xoutput.length;
        console.log("Number of words on truncated from getOutput func:" + tokens);
        // Trả về nội dung email đã xử lý
        resolve(xoutput);
      } else {
        // Nếu có lỗi, ghi log và reject Promise
        console.error(`Error: ${result.error.message}`);
        reject(result.error.message);
      }
    });
  });
}

// Hàm removeKeywords: Loại bỏ các từ khóa (thường là phần chữ ký email) ra khỏi nội dung email.
// emailBody: Nội dung email đầu vào.
// keywords: Mảng các từ khóa cần loại bỏ.
function removeKeywords(emailBody, keywords) {
  let foundKeyword = true; // Biến cờ để kiểm tra xem có tìm thấy từ khóa nào không
  // Lặp cho đến khi không tìm thấy từ khóa nào nữa
  while (foundKeyword) {
    foundKeyword = false;
    // Duyệt qua từng từ khóa trong danh sách
    for (let keyword of keywords) {
      // Nếu tìm thấy từ khóa trong emailBody
      if (emailBody.includes(keyword)) {
        foundKeyword = true; // Đặt lại cờ
        let keywordIndex = emailBody.indexOf(keyword); // Vị trí của từ khóa
        // Tìm vị trí của "From:" sau từ khóa (để giữ lại phần email được quote nếu có)
        let fromIndex = emailBody.indexOf("From:", keywordIndex);
        if (fromIndex !== -1) {
          // Nếu tìm thấy "From:", cắt bỏ phần từ khóa đến trước "From:"
          emailBody = emailBody.substring(0, keywordIndex) + emailBody.substring(fromIndex);
        } else {
          // Nếu không tìm thấy "From:", cắt bỏ toàn bộ phần từ khóa trở đi
          emailBody = emailBody.substring(0, keywordIndex);
        }
        break; // Thoát vòng lặp for sau khi xử lý một từ khóa
      }
    }
  }
  return emailBody; // Trả về nội dung email đã được làm sạch
}

// Hàm aiPrompt: Gửi yêu cầu đến Azure OpenAI API, sử dụng cấu hình động.
// modelIdentifier: Tên định danh của model trong AI_MODELS_CONFIG (ví dụ: "gpt4o").
// systemRoleContent: Vai trò của hệ thống.
// instructionPrompt: Hướng dẫn chính cho AI.
// emailBodyContent: Nội dung email (có thể null).
async function aiPrompt(modelIdentifier, systemRoleContent, instructionPrompt, emailBodyContent) {
  const modelConfig = AI_MODELS_CONFIG[modelIdentifier];

  if (!modelConfig) {
    const errorMessage = `Error: AI model configuration for "${modelIdentifier}" not found.`;
    console.error(errorMessage);
    throw new Error(errorMessage);
  }

  const { apiKey, endpoint } = modelConfig;

  // Tạo đối tượng Headers cho request
  const headers = new Headers();
  headers.append("Content-Type", "application/json");
  headers.append("api-key", apiKey);

  // Xây dựng nội dung prompt đầy đủ cho AI
  let fullUserPrompt = instructionPrompt;
  if (emailBodyContent && emailBodyContent.trim() !== "") {
    fullUserPrompt += (instructionPrompt.endsWith(" ") ? "" : " ") + emailBodyContent;
  }

  // Tạo body cho request, chứa messages (system role và user prompt)
  const body = JSON.stringify({
    messages: [
      {
        role: "system",
        content: systemRoleContent
      },
      {
        role: "user", // Corrected to "user" for the actual user prompt
        content: fullUserPrompt
      }
    ],
    temperature: 0.7, // Kiểm soát mức độ ngẫu nhiên của AI
    max_tokens: 3000 // Số lượng token tối đa cho phản hồi
  });

  try {
    // Gửi request đến API
    const response = await fetch(endpoint, {
      method: "POST",
      headers: headers,
      body: body
    });

    // Kiểm tra nếu request không thành công
    if (!response.ok) {
      const errorBodyText = await response.text();
      const errorMessage = `Network response was not ok: ${response.status} ${response.statusText}. Model: ${modelIdentifier}. Response body: ${errorBodyText}`;
      console.error(errorMessage);
      throw new Error(errorMessage);
    }

    // Parse kết quả JSON từ response
    const json = await response.json();

    // Kiểm tra định dạng của JSON response
    if (!json.choices || !json.choices[0] || !json.choices[0].message || !json.choices[0].message.content) {
      const errorMessage = `Invalid response format from AI service for model: ${modelIdentifier}`;
      console.error(errorMessage);
      throw new Error(errorMessage);
    }

    // Lấy nội dung text từ AI response
    const text = json.choices[0].message.content;
    return text; // Trả về kết quả từ AI
  } catch (error) {
    // Errors are logged where they are thrown or in the calling function's catch block
    throw error;
  }
}

// Hàm aiPrompt4: Gửi yêu cầu đến Azure OpenAI API, sử dụng cấu hình động.
// modelIdentifier: Tên định danh của model trong AI_MODELS_CONFIG (ví dụ: "kinkin4o").
// systemRoleContent: Vai trò của hệ thống.
// instructionPrompt: Hướng dẫn chính cho AI.
// emailBodyContent: Nội dung email (có thể null).
async function aiPrompt4(modelIdentifier, systemRoleContent, instructionPrompt, emailBodyContent) {
  const modelConfig = AI_MODELS_CONFIG[modelIdentifier];

  if (!modelConfig) {
    const errorMessage = `Error: AI model configuration for "${modelIdentifier}" not found.`;
    console.error(errorMessage);
    throw new Error(errorMessage);
  }

  const { apiKey, endpoint } = modelConfig;

  // Tạo đối tượng Headers cho request
  const headers = new Headers();
  headers.append("Content-Type", "application/json");
  headers.append("api-key", apiKey);

  // Xây dựng nội dung prompt đầy đủ cho AI
  let fullUserPrompt = instructionPrompt;
  if (emailBodyContent && emailBodyContent.trim() !== "") {
    // Nối nội dung email vào prompt. Đảm bảo có khoảng trắng nếu instructionPrompt không kết thúc bằng khoảng trắng.
    fullUserPrompt += (instructionPrompt.endsWith(" ") ? "" : " ") + emailBodyContent;
  }

  // Tạo body cho request
  const body = JSON.stringify({
    messages: [
      {
        role: "system",
        content: systemRoleContent
      },
      {
        role: "user", // Đã sửa: vai trò "user" cho prompt thực tế của người dùng
        content: fullUserPrompt
      }
    ],
    temperature: 0.7, // Cân nhắc việc tham số hóa nếu cần thay đổi thường xuyên
    max_tokens: 3000  // Cân nhắc việc tham số hóa
  });

  try {
    // Gửi request đến API
    const response = await fetch(endpoint, {
      method: "POST",
      headers: headers,
      body: body
    });

    // Kiểm tra nếu request không thành công
    if (!response.ok) {
      const errorBodyText = await response.text(); // Lấy thêm chi tiết lỗi từ body
      const errorMessage = `Network response was not ok: ${response.status} ${response.statusText}. Model: ${modelIdentifier}. Response body: ${errorBodyText}`;
      console.error(errorMessage);
      throw new Error(errorMessage);
    }

    // Parse kết quả JSON từ response
    const json = await response.json();

    // Kiểm tra định dạng của JSON response
    if (!json.choices || !json.choices[0] || !json.choices[0].message || !json.choices[0].message.content) {
      const errorMessage = `Invalid response format from AI service for model: ${modelIdentifier}`;
      console.error(errorMessage);
      throw new Error(errorMessage);
    }

    // Lấy nội dung text từ AI response
    const text = json.choices[0].message.content;
    return text; // Trả về kết quả từ AI
  } catch (error) {
    // Xử lý lỗi nếu có (bao gồm cả lỗi từ throw new Error ở trên)
    // Không cần console.error lại ở đây nếu đã log ở nơi throw
    throw error; // Ném lại lỗi để hàm gọi có thể xử lý
  }
}

// Thư viện Showdown (đã comment lại) có thể dùng để chuyển đổi Markdown sang HTML một cách mạnh mẽ hơn.
//import showdown from "https://cdnjs.cloudflare.com/ajax/libs/showdown/1.9.0/showdown.min.js";

// Hàm plainTextToHtml: Chuyển đổi văn bản thuần túy (có thể chứa một số cú pháp Markdown đơn giản) sang HTML.
// text: Văn bản đầu vào.
function plainTextToHtml(text) {
  // Thay thế ký tự xuống dòng bằng thẻ <br>
  var html = text.replace(/\n/g, "<br>");
  // Gọi hàm convertMarkdownToHTML để xử lý các cú pháp Markdown cơ bản
  var xx = convertMarkdownToHTML(html);
  // Bọc kết quả trong thẻ <p> với style Calibri, font size 16px
  html = '<p style="font-family: Calibri; font-size: 16px;">' + xx + "</p>";

  return html; // Trả về chuỗi HTML
}

// Hàm convertMarkdownToHTML: Chuyển đổi một số cú pháp Markdown cơ bản sang HTML.
// markdownText: Văn bản Markdown đầu vào.
function convertMarkdownToHTML(markdownText) {
  // Định nghĩa các biểu thức chính quy (regex) cho các cú pháp Markdown
  const regex = {
    bold: /\*\*(.*?)\*\*/g,        // In đậm: **text**
    italic: /_(.*?)_/g,          // In nghiêng: _text_
    header1: /^# (.*)/gm,         // Tiêu đề cấp 1: # text
    header2: /^## (.*)/gm,        // Tiêu đề cấp 2: ## text
    header3: /^### (.*)/gm,       // Tiêu đề cấp 3: ### text
    link: /\[([^\[]+)\]\(([^)]+)\)/g, // Liên kết: [text](url)
    listItem: /^- (.*)/gm        // Mục danh sách: - text
  };

  // Thực hiện thay thế các cú pháp Markdown bằng thẻ HTML tương ứng
  const htmlText = markdownText
    .replace(regex.bold, "<strong>$1</strong>")
    .replace(regex.italic, "<em>$1</em>")
    .replace(regex.header3, "<h3>$1</h3>")
    .replace(regex.header2, "<h2>$1</h2>")
    .replace(regex.header1, "<h1>$1</h1>")
    .replace(regex.link, '<a href="$2">$1</a>')
    .replace(regex.listItem, "<li>$1</li>");

  // Bọc kết quả trong thẻ <div>
  return `<div>${htmlText}</div>`;
}
