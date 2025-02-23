
# CodeSnippet
The CodeSnippet component is a React component that take code text and language as props and displays it inside a syntax-highlighted code block. It allows users to edit the fetched code and copy it to the clipboard.


## Image
![image](https://github.com/user-attachments/assets/cd816003-2d2c-4aed-9134-cdb2fbce44d7)


## How to Add in your Project 

1. Install react-syntax-highlighter:
   ```sh
   npm install react-syntax-highlighter
2. Create a CodeSnippetWithAPI Component and add code of CodeSnippetWithAPI :
    ```sh
    import React, { useState, useEffect } from "react";
    import { Prism as SyntaxHighlighter } from "react-syntax-highlighter";
    import { atomDark } from "react-syntax-highlighter/dist/esm/styles/prism";
    
    const CodeSnippet = ({ language, code }) => {
      const [uCode, setCode] = useState(code || ""); // Ensure initialCode is used correctly
      const [copied, setCopied] = useState(false);
      const [isEditing, setIsEditing] = useState(false);
    
      const handleCopy = async () => {
        try {
          await navigator.clipboard.writeText(uCode);
          setCopied(true);
          setTimeout(() => setCopied(false), 2000);
        } catch (error) {
          console.error("Failed to copy:", error);
        }
      };
    
      return (
        <div
          style={{
            position: "relative",
            border: "1px solid #444",
            borderRadius: "5px",
            overflow: "hidden",
            padding: "10px",
          }}
        >
          <div
            style={{
              display: "flex",
              justifyContent: "flex-end",
              gap: "10px",
              marginBottom: "10px",
            }}
          >
            <button
              onClick={() => setIsEditing(!isEditing)}
              style={{
                background: "#007bff",
                color: "#fff",
                border: "none",
                padding: "5px 10px",
                borderRadius: "5px",
                cursor: "pointer",
              }}
            >
              {isEditing ? "Save" : "Edit"}
            </button>
    
            <button
              onClick={handleCopy}
              style={{
                background: copied ? "#4CAF50" : "#333",
                color: "#fff",
                border: "none",
                padding: "5px 10px",
                borderRadius: "5px",
                cursor: "pointer",
              }}
            >
              {copied ? "Copied!" : "Copy"}
            </button>
          </div>
    
          {isEditing ? (
            <textarea
              value={uCode}
              onChange={(e) => setCode(e.target.value)}
              style={{
                width: "100%",
                height: "200px",
                fontFamily: "monospace",
                fontSize: "14px",
                padding: "10px",
                border: "1px solid #ccc",
                borderRadius: "5px",
              }}
            />
          ) : (
            <SyntaxHighlighter language={language} style={atomDark}>
              {uCode}
            </SyntaxHighlighter>
          )}
        </div>
      );
    };
    
    export default CodeSnippet;

   
3. Use the Component in Your Project and pass API as props:
   ```sh
   <CodeSnippet
        language="javascript"
        initialCode={`console.log("Hello, World!");`}
      />


### thats all..
