官方文档：[http://www.dropzonejs.com/](http://www.dropzonejs.com/)

Github: [https://github.com/enyo/dropzone](https://github.com/enyo/dropzone)

> DropzoneJS is an open source library that provides drag’n’drop file uploads with image previews.

>It’s lightweight, doesn’t depend on any other library (like jQuery) and is highly customizable.

## 安装
你可能只需要看看简单的[例子](http://www.dropzonejs.com/examples/simple.html)( [源代码](https://github.com/enyo/dropzone/blob/gh-pages/examples/simple.html) )就能开始了。然后继续阅读下面的一步步的指示和不同的安装方法。

下载独立的[dropzone.js](https://raw.github.com/enyo/dropzone/master/dist/dropzone.js)文件。然后这样引入到html中：
```
<script src="./path/to/dropzone.js"></script>
```
Dropzone 现在激活和可用,通过`window.Dropzone`就可以使用了。

> Dropzone不处理你的文件上传在服务器上。你必须自己实现代码接收和存储文件。有关更多信息,请参见部分[服务器端实现](#服务器端实现)。

完成上面的操作就可以使用 Dropzone ，但是如果你想让它你上传的样式看起来像[官方](http://www.dropzonejs.com/)页面那样,你需要将下载的dropzones里面的cs发到你的文件夹中并引入。

#### With component
如果你使用[component](https://github.com/component/component),你只需添加dropzone依赖：
```
"enyo/dropzone": "*"
```
然后这样引入：
```
var Dropzone = require("dropzone");
```
现在它已激活，并可以在页面中使用。
基本的CSS样式也包含在组件中，如果你想让它你上传的样式看起来像[官方](http://www.dropzonejs.com/)页面那样,你需要将下载的dropzones里面的cs发到你的文件夹中并引入。

#### With RequireJS
Dropzone 同样为[RequireJS](http://requirejs.org/)提供了[AMD](https://github.com/amdjs/amdjs-api/wiki/AMD)模块。

你可以在下载的文件夹中找到[dropzone-amd-module](https://raw.github.com/enyo/dropzone/master/dist/dropzone-amd-module.js)。

## 使用
使用 dropzone 的典型的方式是通过创建一个表单包含与`class="dropzone"`:
```
<form action="/file-upload" class="dropzone" id="my-awesome-dropzone">
    <input type="file" name="file" />
</form>
```
就像这样。dropzone 会通过`class`为`dropzone`找到所有的表单元素，并自动将这些元素初始化，然后点击`input`选择文件(或拖拽)之后会根据`action`指定的地址上传文件。(其实就和普通的文件上传没什么区别，只不过多了个拖拽)

如果你想在后端接受文件的时候用其他的`name`而不是上面指定的`file`，您可以配置dropzone的[paramName](#配置选项)的选项。

如果你是使用`component`形式，别忘了`require("dropzone");`,否则是不会生效的。

如果是使用form表单，完成上面的设置之后，就已经可以拖拽上传了，所以如果你不想在写一些js去控制上传中的其他东西，比如进度条、预览区域等，可以在form内加一个包含`fallback`类的标签，dropzone 会自己处理`fallback`类的标签区域，当然这是需要浏览器支持。如果浏览器不支持，那么那就将其作为普通的文件上传。
这通常是这样的：
```
<form action="/file-upload" class="dropzone">
  <div class="fallback">
    <input name="file" type="file" multiple />
  </div>
</form>
```

#### 手动创建dropzones
除了直接在form表单中添加`class`为`dropzone`让其自动创建外，还可以在非表单元素上面通过实例化Dropzone类实现。
```
<div id="myId" style="width: 800px; height: 300px;"></div>
// Dropzone class:
var myDropzone = new Dropzone("div#myId", { url: "/file/post"});
```
或如果您使用jQuery,您可以使用jQuery插件Dropzone形式：
```
// jQuery
$("div#myId").dropzone({ url: "/file/post" });
```
* <span style="color: red">注意：如果你不是使用一个表单元素,别忘了指定一个url选项,因为Dropzone不知道上传到那里。</span> *

#### 服务器端实现
Dropzone 不提供的服务器端文件处理的代码,但是文件上传的方式是和简单的表单文件上传是相同的。比如普通的表单上传是这样：
```
<form action="" method="post" enctype="multipart/form-data">
  <input type="file" name="file" />
</form>
```
掌握基本的服务器上的文件上传,请查看各种语言相应的文档。这里有一些基本的实现文件：

+ [AngularJS and Spring](http://www.cantangosolutions.com/blog/Easy-File-Upload-Using-DropzoneJS-AngularJs-And-Spring)
+ [NodeJS with express](http://howtonode.org/really-simple-file-uploads)
+ [Ruby on rails](http://guides.rubyonrails.org/form_helpers.html#uploading-files)
+ [Complete PHP](http://www.startutorial.com/articles/view/how-to-build-a-file-upload-form-using-dropzonejs-and-php) tutorial by startutorial.com
+ [Basic PHP file upload](http://www.php.net/manual/en/features.file-upload.post-method.php#example-354)
+ [Tutorial for Dropzone and Lavarel (PHP)](http://maxoffsky.com/code-blog/howto-ajax-multiple-file-upload-in-laravel/) written by Maksim Surguy
+ [Symfony2 and Amazon S3](http://www.jesuisundev.fr/upload-drag-drop-via-dropzonejs-symfony2-on-cloud-amazon-s3/)
+ [File upload in ASP.NET MVC using Dropzone JS and HTML5](http://venkatbaggu.com/file-upload-in-asp-net-mvc-using-dropzone-js-and-html5/)

付费的文档：

+ [eBook for Dropzone with PHP](http://www.startutorial.com/homes/dropzonejs_php_the_complete_guide?utm_source=dzj&utm_medium=banner&utm_campaign=dropzonejs) by startutorial.com.

如果你需要更多的信息,请看看[Dropzone FAQ](https://github.com/enyo/dropzone/wiki/FAQ)。

## 配置
有两种方式配置 dropzone：
###### 方法一：
在html元素上添加`dropzone` 样式类，然后就不需要手动使用js去实例化了，但是你的一些配置`Dropzone.options`对象去配置：
```
// "myAwesomeDropzone" 是那个 HTML 元素的 ID
// 这里的id不是驼峰格式，是以`-`为分隔，如 id="my-awesome-dropzone"
Dropzone.options.myAwesomeDropzone = {
  paramName: "file", // The name that will be used to transfer the file
  maxFilesize: 2, // MB
  accept: function(file, done) {
    if (file.name == "justinbieber.jpg") {
      done("Naha, you don't.");
    }
    else { done(); }
  }
};
```

###### 方法二：
最明显的方式是通过一个选择对象时实例化一个dropzone，以前面[手动创建dropzones](#手动创建dropzones)的方式。

###### 常用方法：
因为我们需要使用dropzone提供的一些样式，比如预览时图片样式等，这样就算手动创建，但也需要使用到`dropzone` 样式类，那这样就会导致初始化两次，在控制台就会报错，这时候就需要在手动初始化之前设置如下代码：
```
// Prevent Dropzone from auto discovering this element:
Dropzone.options.myAwesomeDropzone = false;
// This is useful when you want to create the
// Dropzone programmatically later

// Disable auto discover for all elements:
Dropzone.autoDiscover = false;
```
例子：
```
<div class="dropzone" id="myDropzone">
    <div class="am-text-success dz-message">
        将文件拖拽到此处<br>或点此打开文件管理器选择文件
    </div>
</div>

<script type="text/javascript">
    Dropzone.autoDiscover = false;
    var myDropzone = new Dropzone("#myDropzone", {
        url: "/file/upload",
        addRemoveLinks: true,
        method: 'post',
        filesizeBase: 1024,
        sending: function(file, xhr, formData) {
            formData.append("filesize", file.size);
        },
        success: function (file, response, e) {
            var res = JSON.parse(response);
            if (res.error) {
                $(file.previewTemplate).children('.dz-error-mark').css('opacity', '1')
            }
        }
    });
</script>
```
像上面这样，既能使用 dropzone 的样式，也能自己手动初始化上传。

#### 配置选项

<table>
    <tr>
        <th>参数</th>
        <th>描述</th>
    </tr>
    <tr>
        <td id="config-url">url</td>
        <td>除了form元素以外的其他元素必须指定该参数(或当form元素没有操作属性)。您还可以提供一个函数,参数为`files`以及必须返回url(since v3.12.0)</td>
    </tr>
    <tr>
        <td id="config-method">method</td>
        <td>默认为"post",必要的时候你也可以设置为"put"。 您还可以提供一个函数,参数为`files`以及必须返回这个method(since v3.12.0)</td>
    </tr>
    <tr>
        <td id="config-parallelUploads">parallelUploads</td>
        <td>同时上传多少个文件。(更多信息参见队列文件上传部分)</td>
    </tr>
    <tr>
        <td id="config-maxFilesize">maxFilesize</td>
        <td>单位 MB</td>
    </tr>
    <tr>
        <td id="config-filesizeBase">filesizeBase</td>
        <td>默认1000。这个定义的基础是否应该使用1000或1024来计算文件大小。1000是有效的,因为1000个字节等于1千字节,1024字节= 1 Kibibyte。你可以改变为1024，如果你不在乎的有效性。</td>
    </tr>
    <tr>
        <td id="config-paramName">paramName</td>
        <td>文件上传后端接收的参数名。默认`file`。注意:如果你设置uploadMultiple为true,那么Dropzone会将[]附加到这个名字，也就是后端接收的是一个file[]数组。</td>
    </tr>
    <tr>
        <td id="config-uploadMultiple">uploadMultiple</td>
        <td>Dropzone是否在一个请求中发送多个文件。如果它设置为true,然后`fallback`部分的`input`元素须有`multiple`属性。这个选项也会触发其他事件(如`processingmultiple`)。有关更多信息,请参见事件部分。</td>
    </tr>
    <tr>
        <td id="config-headers">headers</td>
        <td>一个向服务器发送附加头的对象。如:`headers: { "My-Awesome-Header": "header value" }`</td>
    </tr>
    <tr>
        <td id="config-addRemoveLinks">addRemoveLinks</td>
        <td>这将添加一个链接到每个文件，删除或取消预览文件(如果已经上传)。`dictCancelUpload`, `dictCancelUploadConfirmation` and `dictRemoveFile`三个参数可选。</td>
    </tr>
    <tr>
        <td id="config-previewsContainer">previewsContainer</td>
        <td>定义文件预览显示。如果为`null`就使用 Dropzone 默认的。可以使用一段普通的html元素或css选择器。被选择的html元素必须包含`dropzone-previews`样式类确保预览显示正常。</td>
    </tr>
    <tr>
        <td id="config-clickable">clickable</td>
        <td>如果为`true`,dropzone元素本身将是可点击的,如果`false`将不可被点击。此外，还可以是一段普通的html或者css选择器，表示点击该元素触发资源管理器。</td>
    </tr>
    <tr>
        <td id="config-createImageThumbnails">createImageThumbnails</td>
        <td></td>
    </tr>
    <tr>
        <td id="config-maxThumbnailFilesize">maxThumbnailFilesize</td>
        <td>单位 MB。文件名超过这个极限时,缩略图将不会生成。</td>
    </tr>
    <tr>
        <td id="config-thumbnailWidth">thumbnailWidth</td>
        <td>如果为`null`,将使用图像的比例来计算它。</td>
    </tr>
    <tr>
        <td id="config-thumbnailHeight">thumbnailHeight</td>
        <td>与`thumbnailWidth`一样。如果两者都是null,图像将不会调整。</td>
    </tr>
    <tr>
        <td id="config-maxFiles">maxFiles</td>
        <td>如果不为`null`,定义多少个文件将被处理。如果超过,事件`maxfilesexceeded`将被调用。相应地dropzone元素得到了类`dz-max—files-reached`，因此你可以提供视觉反馈。</td>
    </tr>
    <tr>
        <td id="config-resize">resize</td>
        <td>创建调整信息时被调用的函数。`file`作为函数第一个参数，同时必须返回一个对象包含`srcX`, `srcY`, `srcWidth` 、`srcHeight` 和相同的 `trg*`。这些值将被用于`ctx.drawImage()`函数。</td>
    </tr>
    <tr>
        <td id="config-init">init</td>
        <td>Dropzone初始化时调用的函数。你能在这个函数中设置事件侦听器。</td>
    </tr>
    <tr>
        <td id="config-acceptedFiles">acceptedFiles</td>
        <td>`accept`函数默认的实现函数，用于检查文件的mime类型或扩展。这是一个逗号分隔的mime类型和文件扩展名的数组。如。`image/*,application/pdf,.psd`。如果Dropzone是`clickable`,此选项将被用作`accept`函数的参数输入。</td>
    </tr>
    <tr>
        <td id="config-accept">accept</td>
        <td>一个接收`file`和`done`函数作为参数输入的函数。如果`done`函数调用无参数,文件会被处理。如果你在`done`函数中传入了参数(比如错误信息)文件将不会被上传。如果文件太大或不匹配的mime类型这个函数不会调用。</td>
    </tr>
    <tr>
        <td id="config-autoProcessQueue">autoProcessQueue</td>
        <td>当设置为false,你必须自身调用`myDropzone.processQueue()`上传文件。有关更多信息,请参见下面有关处理队列。</td>
    </tr>
    <tr>
        <td id="config-previewTemplate">previewTemplate</td>
        <td>一个字符串,其中包含模板用于每一个图像。改变它满足你的需求,但确保正确地提供所有元素。你可以在页面中建立这样一个容器:`id="preview-template"`(设置style="display: none;"),然后这样设置：`previewTemplate: document.querySelector('preview-template').innerHTML`。</td>
    </tr>
    <tr>
        <td id="config-forceFallback">forceFallback</td>
        <td>默认值为false。如果为true,`fallback`将被强行使用。这是非常有用的测试服务器实现首要方式,确保一切如预期所想，并测试你的`fallback`显示如何。</td>
    </tr>
    <tr>
        <td id="config-fallback">fallback</td>
        <td>当浏览器不支持时调用的函数。默认实现显示了`fallback`内的`input`域并添加一个文本。</td>
    </tr>
    <tr>
        <td colspan="2">为自定义的 dropzone,你也可以使用如下这些选项</td>
    </tr>
    <tr>
        <td id="config-dictDefaultMessage">dictDefaultMessage</td>
        <td>任何文件被拖拽进区域之前显示的信息。这通常是被一个图像,但默认为“Drop files here to upload”。</td>
    </tr>
    <tr>
        <td id="config-dictFallbackMessage">dictFallbackMessage</td>
        <td>如果浏览器不支持,默认消息将被替换为这个文本。默认为“Your browser does not support drag'n'drop file uploads.”。</td>
    </tr>
    <tr>
        <td id="config-dictFallbackText">dictFallbackText</td>
        <td>这将被添加在`input file`之前。如果你提供一个`fallback`元素,或者该选项为空该选项将被忽略。默认为“Please use the fallback form below to upload your files like in the olden days.”。</td>
    </tr>
    <tr>
        <td id="config-dictInvalidFileType">dictInvalidFileType</td>
        <td>如果文件类型不匹配时显示的错误消息。</td>
    </tr>
    <tr>
        <td id="config-dictFileTooBig">dictFileTooBig</td>
        <td>当文件太大时显示。`{{filesize}}`` 和 `{{maxFilesize}}`` 将被替换。</td>
    </tr>
    <tr>
        <td id="config-dictResponseError">dictResponseError</td>
        <td>如果服务器响应是无效的时显示的错误消息。`{{statusCode}}`` 将被替换为服务器端返回的状态码。</td>
    </tr>
    <tr>
        <td id="config-dictCancelUpload">dictCancelUpload</td>
        <td>如果`addRemoveLinks`为true,文本用于取消上传链接的文字。</td>
    </tr>
    <tr>
        <td id="config-dictCancelUploadConfirmation">dictCancelUploadConfirmation</td>
        <td>如果`addRemoveLinks`为true,文本用于取消上传的文字。</td>
    </tr>
    <tr>
        <td id="config-dictRemoveFile">dictRemoveFile</td>
        <td>如果`addRemoveLinks`为true,用于删除一个文件的文本。</td>
    </tr>
    <tr>
        <td id="config-dictMaxFilesExceeded">dictMaxFilesExceeded</td>
        <td>如果设置了`maxFiles`,这将是超过了设置的时候的错误消息。</td>
    </tr>
</table>
你也可以覆盖所有违约事件动作选项。如果你提供的`drop`选项可以覆盖默认的事件处理程序。你应该熟悉代码,因为您可以轻松掌握这样的上传。如果你只是想做额外修改,比如添加一些过滤什么的，可以[监听事件](#事件)。

#### 文件上传队列
当一个文件被添加到dropzone,其`status`被设置到`Dropzone.QUEUED`(`accept`函数检查通过后)，这意味着该文件现在在队列中。

如果你可以选择`autoProcessQueue`设置为`true`,那么队列是立即处理,文件被删除或一个上传完成后,通过调用`.processQueue()`,检查有多少文件正在上传,如果它少于`option.parallelUploads`,`.processFile`将被调用。

如果你`autoProcessQueue`设置为`false`,那么`.processQueue()`不会被隐式地调用。这意味着当你想上传目前队列中所有文件时你必须自己调用它。

#### 布局
为每个文件生成预览HTML，设置dropzone定义的选项`previewTemplate`,默认为：
```
<div class="dz-preview dz-file-preview">
  <div class="dz-details">
    <div class="dz-filename"><span data-dz-name></span></div>
    <div class="dz-size" data-dz-size></div>
    <img data-dz-thumbnail />
  </div>
  <div class="dz-progress"><span class="dz-upload" data-dz-uploadprogress></span></div>
  <div class="dz-success-mark"><span>✔</span></div>
  <div class="dz-error-mark"><span>✘</span></div>
  <div class="dz-error-message"><span data-dz-errormessage></span></div>
</div>
```
当文件在上传过程中的时候，`dz-preview`中的`dz-processing`将被显示；当文件上传之后`dz-success`将被显示；如果文件上传错误或没网`dz-error`将被显示，此时`data-dz-errormessage`的内容将是服务器端返回的信息。

重写默认的模板，就可以使用配置中的`previewTemplate`选项。

您可以通过`file.previewElement`访问文件的HTML预览,并且设置任何事件。如：
```
success: function (file, response, e) {
    var res = JSON.parse(response);
    if (res.error) {
        $(file.previewTemplate).children('.dz-error-mark').css('opacity', '1')
    }
}
```
如果你想打破常规重写`previewElement`,可以在你想要的元素上添加`data-dz-*`属性：

+ data-dz-name
+ data-dz-size
+ data-dz-thumbnail (这个必须是 `<img />` 元素，然后该元素的 `alt` 和 `src` 属性会被 Dropzone 自动改变为相应的值)
+ data-dz-uploadprogress (当文件处于上传过程中的时候Dropzone 将改变此元素的 `style.width` 的值，从 0% 到 100%)
+ data-dz-errormessage
Dropzone将寻找这些元素，并改变默认选项和更新它的内容。

如果你想要一些特定链接删除一个文件(而不是建于[addRemoveLinks](#config-addRemoveLinks)配置),您可以简单地插入元素的模板data-dz-remove属性。
```
<img src="removebutton.png" alt="Click me to remove the file." data-dz-remove />
```

你也不用被这些使用惯例所强迫。如果你完全覆盖所有默认事件监听器可以从头开始重建你的布局。

如果你想让你的dropzone看起来像[官方](http://www.dropzonejs.com/)页面那样，使用安装部分提供的添加样式表和spritemaps即可。

看到[主题](#主题)部分,看看如何改变Dropzone 的UI。

官方创建了一个例子,配置几行代码，让Dropzone看起来和感觉完全和jQuery文件上传差不多。[Check it out!](http://www.dropzonejs.com/bootstrap.html)

#### Dropzone方法
如果你想删除已添加的文件,你可以调用`.removeFile(file)`。这种方法也触发`removedfile`事件。

下面是一个示例,文件上传完成后将自动删除：
```
myDropzone.on("complete", function(file) {
  myDropzone.removeFile(file);
});
```
如果你想删除所以的文件，简单地使用`.removeAllFiles()`。正在上传中的文件不会被删除。如果你想取消正在上传的文件，调用`.removeAllFiles(true)`将取消上传。

如果你设置了`autoProcessQueue`为`false`,你必须调用.processQueue()实现上传。

访问dropzone中的所有文件,使用`myDropzone.files`。

+ 所有可接受的文件：`.getAcceptedFiles()`
+ 所以被拒绝的文件：`.getRejectedFiles()`
+ 队列中的所有文件：`.getQueuedFiles()`
+ 上传中的所有文件：`.getUploadingFiles()`
如果不在需要一个dropzone,使用当前示例调用`.disable()`，这将移除该元素上的事件、文件。重新激活使用`.enable()`。`

如果你不喜欢浏览器默认的`confirm`,您可以通过覆盖`Dropzone.confirm`处理它们:
```
Dropzone.confirm = function(question, accepted, rejected) {
  // Ask the question, and call accepted() or rejected() accordingly.
  // CAREFUL: rejected might not be defined. Do nothing in that case.
};
```

## 事件
Dropzone触发事件在处理文件时,你可以通过当前实例调用`.on(eventName, callbackFunction)`监听事件。

因为听事件只能是Dropzone实例,设置你的事件侦听器,最好的地方是在init函数。
```
Dropzone.options.myAwesomeDropzone = {
  init: function() {
    this.on("addedfile", function(file) { alert("Added file."); });
  }
};
```
如果你[手动创建dropzones](#手动创建dropzones),你可以设置实例的事件监听器,就像这样:
```
// This example uses jQuery so it creates the Dropzone, only when the DOM has
// loaded.

// Disabling autoDiscover, otherwise Dropzone will try to attach twice.
Dropzone.autoDiscover = false;
// or disable for specific dropzone:
// Dropzone.options.myDropzone = false;

$(function() {
  // Now that the DOM is fully loaded, create the dropzone, and setup the
  // event listeners
  var myDropzone = new Dropzone("#my-dropzone");
  myDropzone.on("addedfile", function(file) {
    /* Maybe display some more file information on your page */
  });
})
```

这是更复杂的,没有必要的,除非你有一个很好的理由来管理实例化Dropzones。

Dropzone本身严重依赖事件，视觉上的展示都是通过监听去做的。这些事件监听器设置在每个Dropzone的默认配置,可以覆盖,从而取代默认的行为实现自己的事件回调。

#### 事件列表

<table>
    <tr>
        <td colspan="2">不覆盖这些配置选项,除非你知道你在做什么。</td>
    </tr>
    <tr>
        <th>事件</th>
        <th>描述</th>
    </tr>
    <tr>
        <td colspan="2">所有这些接收`event`作为第一个参数</td>
    </tr>
    <tr>
        <td id="event-drop">drop</td>
        <td>用户松放文件到到dropzone</td>
    </tr>
    <tr>
        <td id="event-dragstart">dragstart</td>
        <td>用户开始拖动文件到任何地方</td>
    </tr>
    <tr>
        <td id="event-dragend">dragend</td>
        <td>拖动结束</td>
    </tr>
    <tr>
        <td id="event-dragenter">dragenter</td>
        <td>用户拖拽文件到Dropzone</td>
    </tr>
    <tr>
        <td id="event-dragover">dragover</td>
        <td>用户拖动一个文件经过Dropzone</td>
    </tr>
    <tr>
        <td id="event-dragleave">dragleave</td>
        <td>用户拖动一个文件离开Dropzone</td>
    </tr>
    <tr>
        <td colspan="2">所有这些接收`file`作为第一个参数</td>
    </tr>
    <tr>
        <td id="event-addedfile">addedfile</td>
        <td>当一个文件被添加到列表中</td>
    </tr>
    <tr>
        <td id="event-removedfile">removedfile</td>
        <td>从列表中删除一个文件。你可以监听该事件然后从您的服务器删除文件</td>
    </tr>
    <tr>
        <td id="event-thumbnail">thumbnail</td>
        <td>生成缩略图。接收`dataUrl`作为第二个参数</td>
    </tr>
    <tr>
        <td id="event-error">error</td>
        <td>发生一个错误。接收`errorMessage`作为第二个参数,如果错误是由于XMLHttpRequest `xhr`对象为第三个参数。</td>
    </tr>
    <tr>
        <td id="event-processing">processing</td>
        <td>当一个文件被处理(因为队列不会立即处理所有文件)。这个事件在`processingfile`之前被触发。</td>
    </tr>
    <tr>
        <td id="event-uploadprogress">uploadprogress</td>
        <td>每当文件上载过程变化是触发。获得`progress`作为第二个参数，是一个百分比(0 - 100)和`bytesSent`作为第三个参数，是已经发送到服务器的字节数量。当上传完成`dropzone`确保`uploadprogress`为100%并被调用一次。Warning：这个函数可以调用多次使用相同的`progress`。</td>
    </tr>
    <tr>
        <td id="event-sending">sending</td>
        <td>在每个文件发送是触发。`file`为第一个参数，`xhr`对象和`formData`对象作为第二个和第三个参数,你可以修改它们(例如添加CSRF令牌)或添加额外的数据。</td>
    </tr>
    <tr>
        <td id="event-success">success</td>
        <td>文件已经成功上传触发。`file`为第一个参数，获取服务器响应作为第二个参数。(这一事件在`finished`之前触发。</td>
    </tr>
    <tr>
        <td id="event-complete">complete</td>
        <td>上传成功或错误时。</td>
    </tr>
    <tr>
        <td id="event-canceled">canceled</td>
        <td>当一个文件上传被取消时。</td>
    </tr>
    <tr>
        <td id="event-maxfilesreached">maxfilesreached</td>
        <td>文件数量接受到达maxFiles极限时</td>
    </tr>
    <tr>
        <td id="event-maxfilesexceeded">maxfilesexceeded</td>
        <td>每个文件被拒绝了,因为文件的数量超过了maxFiles极限时触发</td>
    </tr>
    <tr>
        <td></td>
        <td></td>
    </tr>
    <tr>
        <td colspan="2">所有这些收到的`files`作为第一个参数,并且就当`uploadMultiple`为`true`时触发</td>
    </tr>
    <tr>
        <td id="event-processingmultiple">processingmultiple</td>
        <td>见`processing`的描述。</td>
    </tr>
    <tr>
        <td id="event-sendingmultiple">sendingmultiple</td>
        <td>见`sending`的描述。</td>
    </tr>
    <tr>
        <td id="event-successmultiple">successmultiple</td>
        <td>见`success`的描述。</td>
    </tr>
    <tr>
        <td id="event-completemultiple">completemultiple</td>
        <td>见`complete`的描述。</td>
    </tr>
    <tr>
        <td id="event-canceledmultiple">canceledmultiple</td>
        <td>见`canceled`的描述。</td>
    </tr>
    <tr>
        <td colspan="2">特殊事件</td>
    </tr>
    <tr>
        <td id="event-totaluploadprogress">totaluploadprogress</td>
        <td>触发时包含参数`total uploadProgress(0 - 100)`,`totalBytes`和`totalBytesSent`。这个事件可以用来显示所有文件的整体上载进度</td>
    </tr>
    <tr>
        <td id="event-reset">reset</td>
        <td>调用时列表中的所有文件被删除,dropzone重置为初始状态。</td>
    </tr>
    <tr>
        <td id="event-queuecomplete">queuecomplete</td>
        <td>当队列中的所有文件上传完成时。</td>
    </tr>
</table>

#### 主题
如果你想对Dropzone的主题完全自定义,在大多数情况下,您可以简单地取代HTML模板预览,调整CSS,也可以创建一些额外的事件监听器。

官方创建了一个例子,配置几行代码，让Dropzone看起来和感觉完全和jQuery文件上传差不多。[Check it out!](http://www.dropzonejs.com/bootstrap.html)。正如您可以看到的,最大的变化就是previewTemplate。然后添加了一些额外的事件监听器来让它看起来符合自己的要求。

然而,您可以完全从头开始实现您的UI。

覆盖默认的事件监听器,创建您自己的自定义Dropzone,可以这样：
```
// This is an example of completely disabling Dropzone's default behavior.
// Do *not* use this unless you really know what you are doing.
Dropzone.myDropzone.options = {
  previewTemplate: document.querySelector('#template-container').innerHTML,
  // Specifing an event as an configuration option overwrites the default
  // `addedfile` event handler.
  addedfile: function(file) {
    file.previewElement = Dropzone.createElement(this.options.previewTemplate);
    // Now attach this new element some where in your page
  },
  thumbnail: function(file, dataUrl) {
    // Display the image in your file.previewElement
  },
  uploadprogress: function(file, progress, bytesSent) {
    // Display the progress
  }
  // etc...
};
```
上面的这些代码显然缺乏实际的实现。看源代码,看看Dropzone内部的实现。

如果你不需要任何默认Dropzone UI，只对Dropzone的事件处理程序、文件上传和拖拽功能感兴趣,那你应该使用以上选项事件处理。

## Tips
如果你不想要默认消息提示(拖拽文件上传(或单击)),您可以在你`dropzone`元素内添加一个元素包含类`dz-message`，这样`dropzone`就不会为您创建的消息。
***
Dropzone 或提交你设置的`form`内的所有隐藏的表单域信息。所以当你是使用`form`元素的形式的话，这是一个简单的方法来提交额外的数据，至于是`get`还是`post`取决于你`form`的`method`。当然也可以在js配置中添加其他的参数。
***
当事件绑定完成之后，Dropzone 会添加数据到`file`对象。如果是`image`的话，你可以通过`file.width` 和 `file.height`访问到图片的宽度和高度。而且`file.upload`对象会包含如下信息：`progress` (0-100), `total` (总字节) and `bytesSent`（已上传字节）。这样你可以通过这写信息自定义上传进度条等。
***
如果你想给上传的文件添加额外（多个文件时会具体到每个文件）,您可以注册发送事件：
```
myDropzone.on("sending", function(file, xhr, formData) {
  // Will send the filesize along with the file as POST data.
  formData.append("filesize", file.size);
});
```
***
文件上传之后，可以通过`file.previewElement`访问上传后文件的预览html。例如：
```
myDropzone.on("addedfile", function(file) {
  file.previewElement.addEventListener("click", function() {
    myDropzone.removeFile(file);
  });
});
```
***
如果你想整个的`body`都是一个`Dropzone`实例而且在某个地方显示文件预览，那你可以简单地为`body`实例化一个Dropzone对象，提示定义`previewsContainer` 选项。这个`previewsContainer`可以是`dropzone-previews`或`dropzone`类，以便正确显示文件预览：
```
new Dropzone(document.body, {
  previewsContainer: ".dropzone-previews",
  // You probably don't want the whole body
  // to be clickable to select files
  clickable: false
});
```
***
可以在[github wiki](https://github.com/enyo/dropzone/wiki)寻找更多的例子。

## 兼容性
本节描述Dropzone兼容浏览器和旧版本。
#### 浏览器支持:

+ Chrome 7+
+ Firefox 4+
+ IE 10+
+ Opera 12+ (MacOS V12版本无法使用，因为它的API有问题)
+ Safari 6+

对于所有其他浏览器,dropzone提供一个版的文件输入回退。
在老式浏览器中`拖放`是没有解决方案，毕竟它不支持嘛~~,其次dropzone的图片预览也是同样的道理。
但是，用户使用老式浏览器还是可以上传文件滴，只是看起来和感觉起来都不是很棒。
哎,年代已经不属于它们了。

#### Version 4.0
<small><i>这不是一个更新日志。只列出兼容性问题。</i></small>

+ 改变默认[previewTemplate](#config-previewTemplate)。布局做了新调整[layout sectin](#布局).
+ 使用SVG代替PNG spritemap(CSS文件现在唯一需要包括的附加文件)

#### Version 3.0
<small><i>这不是一个更新日志。只列出兼容性问题。</i></small>


#### Version 2.0
<small><i>这不是一个更新日志。只列出兼容性问题。</i></small>

从2.0版本开始,Dropzone不再依赖jQuery,如果使用了jQuery，Dropzone 通过jQuery模块的形式加载自身。
这意味着创建Dropzones这样仍能工作：
```
$("#my-dropzone").dropzone({ /* options */ });
```
如果你通过普通构造函数的形式创建Dropzones,你必须通过原始HTMLElement,或者一个选择器字符串选择相应的元素，这样该版本才能运行：
```
// With jQuery
new Dropzone($("#my-dropzone").get(0));
// Without jQuery
new Dropzone("#my-dropzone");
new Dropzone(document.querySelector("#my-dropzone"));
```
另外一个改变就是，Dropzone不再存储实例内部元素的数据属性。为了得到一个dropzone元素这样做：
```
// DEPRECATED, do not use:
$("#my-dropzone").data("dropzone"); // won't work anymore
// Do this now:
Dropzone.forElement(element); // Providing a raw HTMLElement
// or
Dropzone.forElement("#my-dropzone"); // Providing a selector string.
```

## About me
博客: [http://blog.helloarron.com](http://blog.helloarron.com)

Github: [https://github.com/ArronYR](https://github.com/ArronYR)

Email: yangyun4814@gmail.com