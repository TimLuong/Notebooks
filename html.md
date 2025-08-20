<style>
  body {
    font-family: "Segoe UI", "Segoe UI Web (West European)", "Segoe UI", -apple-system, BlinkMacSystemFont, Roboto, "Helvetica Neue", sans-serif;
    margin: 0;
    padding: 0;
    background-color: #f3f2f1; /* Fluent UI neutralLighter */
    color: #323130; /* Fluent UI neutralPrimary */
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
  }

  .container {
    padding: 16px; /* Adjusted padding */
    max-width: 400px;
    margin: auto;
  }

  .section-title {
    font-size: 18px; /* Fluent UI recommends specific type ramps, this is an approximation */
    font-weight: 600; /* Semibold */
    color: #323130; /* Fluent UI neutralPrimary */
    margin-top: 24px;
    margin-bottom: 12px;
    padding-bottom: 4px;
    border-bottom: 1px solid #e1dfdd; /* Fluent UI neutralQuaternaryAlt */
  }

  .button-grid {
    display: grid;
    grid-template-columns: 1fr;
    gap: 10px; /* Slightly increased gap */
    margin-bottom: 24px;
  }

  .ms-Button {
    width: 100%;
    text-align: left;
    display: flex;
    align-items: center;
    padding: 10px 12px; /* Adjusted padding for a taller button */
    background-color: #ffffff; /* White background */
    border: 1px solid #c8c6c4; /* Fluent UI neutralSecondary */
    border-radius: 4px; /* Fluent UI standard border radius */
    font-size: 14px; /* Standard button text size */
    font-weight: 400; /* Regular weight */
    color: #323130; /* neutralPrimary */
    cursor: pointer;
    transition: background-color 0.2s ease-in-out, box-shadow 0.2s ease-in-out, border-color 0.2s ease-in-out;
  }

  .ms-Button:hover {
    background-color: #f3f2f1; /* neutralLighter */
    border-color: #a19f9d; /* neutralTertiary */
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1); /* Subtle shadow for depth */
  }

  .ms-Button:active {
    background-color: #edebe9; /* neutralLight */
    border-color: #8a8886; /* neutralTertiaryAlt */
    box-shadow: none; /* Remove shadow on active */
  }
  
  .ms-Button:focus {
    outline: 2px solid #0078d4; /* Fluent UI focus outline */
    outline-offset: 1px;
  }


  .ms-Button-label {
    margin-left: 8px;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
  }

  .form-control {
    width: 100%; /* Use 100% and box-sizing */
    padding: 10px;
    border: 1px solid #8a8886; /* neutralSecondary */
    border-radius: 4px; /* Fluent UI standard border radius */
    font-size: 14px;
    min-height: 80px;
    box-sizing: border-box; /* Important for width calculation */
    background-color: #ffffff;
    color: #323130;
    transition: border-color 0.2s ease-in-out;
  }

  .form-control:focus {
    border-color: #0078d4; /* themePrimary */
    outline: none; /* Remove default outline, rely on border */
    box-shadow: 0 0 0 1px #0078d4; /* Focus ring style */
  }
  
  .custom-request-section .ms-Button {
    margin-top: 10px; /* Consistent gap */
    background-color: #0078d4; /* Primary button color */
    color: #ffffff; /* White text for primary button */
    border-color: #0078d4;
  }

  .custom-request-section .ms-Button:hover {
    background-color: #005a9e; /* Darker shade for hover */
    border-color: #005a9e;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  }

  .custom-request-section .ms-Button:active {
    background-color: #004578; /* Even darker for active */
    border-color: #004578;
  }
</style>

<div class="container">
  <h3 class="section-title">📧 Outlook Copilot</h3>

  <div class="button-grid">
    <button id="emailSummarize" class="ms-Button">
      <span class="icon">📝</span>
      <div class="ms-Button-label">Summarize Email</div>
    </button>
    <button id="generalCoaching" class="ms-Button">
      <span class="icon">👨‍🏫</span>
      <div class="ms-Button-label">Coaching Email</div>
    </button>
    <button id="generalCoachingPDP" class="ms-Button">
      <span class="icon">📊</span>
      <div class="ms-Button-label">Coaching PDP</div>
    </button>
  </div>
  
  <div class="custom-request-section section-title">💬 Custom AI Request</div>
  <textarea id="textArea" class="form-control" name="TextArea" placeholder="waiting for your input..." rows="6"></textarea>
  <button id="submitButton" class="ms-Button">
    <span class="icon">🤖</span>
    <div class="ms-Button-label">Your own request to Zumei</div>
  </button>
</div>
