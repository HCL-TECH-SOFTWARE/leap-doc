# Performance Recommendations

The applications that you build can affect the overall health and performance of the {{shortProductName}} server.

1. Inform the server administrator if you expect your application to experience high usage, capture large volumes of data, or collect attachments. Note that Leap is not intended as a file storage application.

2. Applications with service calls incur more overhead.  Choose carefully how and when you use services within your application.

3. Test your application before making it available to your target audience.  This includes:
    - performance testing
    - testing each stage of the workflow
    - testing service calls
    - testing the application such that all conditional paths, via rules or custom javaScript, are verified
    - open the console, which is part of the browser debugging tools, and verify that there are no javaScript errors 
    - open the network tab, which is part of the browser debugging tools, and verify there are no looping service calls

  4. Offload static content by referencing images or files from a central location instead of embedding them within your application. Avoid using {{shortProductName}} to deliver static web pages, as this adds unnecessary overhead and can slow down rendering compared to traditional HTML pages.

  5. If you plan to export your application or its data, schedule the export outside of peak hours to minimize the impact on system performance.

  6. If you have written custom code that exercises the REST API to perform batch updating, make sure your server admin is aware and run the process outside peak hours.

  **Parent topic:** [Building Apps](cr_creating_and_managing_toc.md)

