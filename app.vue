<script setup lang="ts">
import * as Bytescale from "@bytescale/sdk";
import nodeFetch from "node-fetch";


if (process.server) {
  const uploadManager = new Bytescale.UploadManager({
    fetchApi: nodeFetch, // import nodeFetch from "node-fetch"; // Only required for Node.js. TypeScript: 'nodeFetch as any' may be necessary.
    apiKey: "API_KEY_HERE" // This is your API key.
  });

  uploadManager
    .upload({
      // Supported types:
      // - String
      // - Blob
      // - ArrayBuffer
      // - Buffer
      // - ReadableStream (Node.js), e.g. fs.createReadStream("file.txt")
      data: "Hello World",

      // Required if 'data' is a stream, buffer, or string.
      mime: "text/plain",

      // Required if 'data' is a stream, buffer, or string.
      originalFileName: "my_file.txt",

      // Required if 'data' is a stream.
      // size: 5098, // e.g. fs.statSync("file.txt").size
    })
    .then(
      ({ fileUrl, filePath }) => {

        // --------------------------------------------
        // File successfully uploaded!
        // --------------------------------------------
        // The 'filePath' uniquely identifies the file,
        // and is what you should save to your DB.
        // --------------------------------------------
        console.log(`File uploaded to: ${fileUrl}`);

      },
      error => console.error(`Error: ${error.message}`, error)
    );
}
</script>

<template>
  <div>
    <NuxtRouteAnnouncer />
    <NuxtWelcome />
  </div>
</template>
