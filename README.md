# Unsigned Uploads with the Cloudinary Upload Widget

## 3 easy steps to allow your users to upload images and videos to your Cloudinary account.

1. Retrieve your Cloudinary Cloud Name from the Cloudinary Dashboard.
    - This step requires a Cloudinary account, you can sign up for free from [here](https://cloudinary.com/users/register_free).
    - Once logged in, you will see your [Cloud Name prominently displayed in the dashboard](assets/cloudname.png).
    - Copy or remember your Cloud Name; you'll use it in step 3.
2. Create an Unsigned Upload Preset in the settings menu of the Cloudinary Dashboard.
    - From within the Cloudinary dashboard, click the [settings cogwheel](assets/settings-cogwheel.png) in the lower left corner.
    - Click the ["Upload Presets"](assets/upload-presets-menu-option.png) menu option.
    - Click the blue ["+ Add Upload Preset"](assets/add-upload-preset-button.png) button in the top right corner.
    - Now enter in a unique Upload preset name, select the "Unsigned" option from the Signing mode dropdown menu, and click the blue "Save" button in the top right corner ([view screenshot](assets/create-upload-preset.png)).
    - Copy or remember the Upload preset name; you'll use it in step 3.
3. Add the Upload Widget code to your project and replace the placeholder values for both the Cloud Name and Upload Preset.
    - Open your preferred code editor and navigate to the HTML file within your project where you want the Upload Widget to live.
    - Add a button element to the page that will trigger the Upload Widget when clicked. Note the `id` attribute, this is how we will select the button in our custom JavaScript code. Likewise, the `class` adds predetermined styling, but feel free to style it to best suit your project.
        ```HTML
        <button id="upload_widget" class="cloudinary-button">
            Upload files
        </button>
        ```
    - Add the Upload Widget JS file from Cloudinary. This must be included prior to the custom script that follows.
        ```HTML
        <script src="https://widget.cloudinary.com/v2.0/global/all.js" type="text/javascript"></script>
        ```
    - Add the custom JavaScript for intializing the Upload Widget with your custom Cloud Name and Upload Preset as well as any predetermined configurations for appearance and behavior. **Be sure to replace the values for the cloudName and uploadPreset variables with the ones created in steps 1. and 2. of this guide.**
        ```HTML
          <script type="text/javascript">
            const cloudName = "YOUR CLOUD NAME";
            const uploadPreset = "YOUR UPLOAD PRESET";

            const myWidget = cloudinary.createUploadWidget({
                cloudName: cloudName,
                uploadPreset: uploadPreset,
            },
            (error, result) => {
                if (!error && result && result.event === "success") {
                    console.log("Done! Here is the asset info: ", result.info);
                }
            }
            );

            document.getElementById("upload_widget").addEventListener("click",
                function () {
                    myWidget.open();
                }
            );
        </script>
        ```
    - Preview and test the Upload Widget by running your project on a local server with a tool like [Live Server](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer) for [VSCode](https://code.visualstudio.com/).
    - You can reference the [sample project](./index.html) in this repository to ensure you followed all of the steps correctly.