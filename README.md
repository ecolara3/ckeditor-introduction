
# Ckeditor SimpleFileUploader Example

This is a sample of how to integrate CKEditor5 into an Angular Application. While the documentation exists and is fragmented, this example uses a custom build made using the CKEditor online custom build tool, and setup into you Angular Application.

Steps to setup

1. Install CKEditor5 "@ckeditor/ckeditor5-angular"
    -Add the CKEditorModule if your parent module
    ```
    import { CKEditorModule } from '@ckeditor/ckeditor5-angular';

    imports: [...,CKEditorModule ]
    ```
2. Go to the [Custom Build Tool for CKEditor](https://ckeditor.com/ckeditor-5/online-builder/)
    - When choosing Plugins deselect "CKFinder upload adapter" and select "Simple upload adapter"
    - Also select whatever plugins you want here
    - For the "Toolbar" step, select everything you want except CKFinder

3. After downloading build, copy content of build folder to a directory in the src directory of your application

4. In the component you want to use the editor import from the custom build you made via the online tool
```
    import * as ClassicEditor from 'src/ckeditor/ckeditor';
```
5. Add the following to you tsconfig.json file
```
      "compilerOptions": {
            "allowJs": true,
            ...
```
6. Add a public Editor and config property to the component
```
      public Editor = ClassicEditor;
      public config: any;
```
7. In the constructor add the config settings as follows:
```
    this.config = {
      toolbar: {
        items: [
          'bold',
          'italic',
          'link',
          'bulletedList',
          'numberedList',
          'imageUpload',
          'blockQuote',
          'undo',
          'redo'
        ]
      },
      image: {
        toolbar: [
          'imageStyle:full',
          'imageStyle:side',
          '|',
          'imageTextAlternative'
        ]
      },
      simpleUpload: {
        // The URL that the images are uploaded to.
        uploadUrl: 'http://example.com',

        // Enable the XMLHttpRequest.withCredentials property.
        withCredentials: false,

        // Headers sent along with the XMLHttpRequest to the upload server.
        //headers: {
        //  'X-CSRF-TOKEN': 'CSFR-Token',
        //  Authorization: 'Bearer <JSON Web Token>'
        //}
      },
      // This value must be kept in sync with the language defined in webpack.config.js.
      language: 'en'
    };
```
8. Add the editor to the components template
```
    <ckeditor [config]="config" [editor]="Editor"></ckeditor>
```
9. `npm run start`