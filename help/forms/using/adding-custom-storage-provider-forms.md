---
title: 草稿和提交组件的自定义存储
seo-title: 草稿和提交组件的自定义存储
description: 请参阅如何自定义草稿和提交的用户数据存储。
seo-description: 请参阅如何自定义草稿和提交的用户数据存储。
uuid: ac2e80ee-a9c7-44e6-801e-fe5a840cb7f8
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: 154255e7-468a-42e6-a33d-eee691cf854d
feature: Forms Portal
exl-id: b1300eeb-2653-4bb5-b2fd-88048c9c43b9
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 1%

---

# 草稿和提交组件的自定义存储{#custom-storage-for-drafts-and-submissions-component}

## 概述 {#overview}

AEM Forms允许您将表单另存为草稿。 草稿功能允许您维护正在进行的表单，您可以从任何设备完成并稍后提交该表单。

默认情况下，AEM Forms会将与表单草稿和提交相关的用户数据存储在Publish实例的`/content/forms/fp`节点中。 此外，AEM Forms门户组件还提供数据服务，您可以使用这些数据服务来自定义存储草稿和提交用户数据的实施。 例如，您可以将用户数据存储在数据存储中。

## 前提条件  {#prerequisites}

* 启用[forms门户组件](/help/forms/using/enabling-forms-portal-components.md)
* 创建[forms门户页面](/help/forms/using/creating-form-portal-page.md)
* 为表单门户启用[自适应表单](/help/forms/using/draft-submission-component.md)
* 了解自定义存储的[实施详细信息](/help/forms/using/draft-submission-component.md#customizing-the-storage)

## 草稿数据服务{#draft-data-service}

要自定义草稿的用户数据存储，您需要实施`DraftDataService`界面的所有方法。 以下示例代码介绍了方法和参数。

```java
/**
 * DraftDataService service will get/delete/save user data (attachments and form data) filled with a draft instance of Form
 */

public interface DraftDataService {

    /**
     * To save/modify user data for this userDataID, it will be null in case of creation
     * @param draftDataID: unique identifier associated with the form data
     * @param formName: name of the form whose draft is being saved
     * @param formData: user data associated with this draft
     * @return userdataID corresponding to which user data has been stored and which can be used later to retrieve this user data
     * @throws FormsPortalException
     */
    public String saveData (String draftDataID, String formName, String formData) throws FormsPortalException;

    /**
     * Returns the user data stored against the ID passed as the argument
     * @param userDataID: unique data id for user data associated with a draft
     * @return user data associated with this data ID
     * @throws FormsPortalException
     */

    public byte[] getData (String userDataID) throws FormsPortalException;

    /**
     * To delete data associated with this draft
     * @param userDataID: unique data id for data associated with a draft
     * @return status of delete operation on data associated with this draft
     * @throws FormsPortalException
     */

    public boolean deleteData (String userDataID) throws FormsPortalException;

    /**
     * Saves the attachment for current form instance
     * @param attachmentsBytes: byte array of the attachment to be saved
     * @return unique id (attachmentID) for the attachment just saved (so that it could be retrieved later)
     * @throws FormsPortalException
     */
    public String saveAttachment (byte[] attachmentBytes) throws FormsPortalException;

    /**
     * To delete an attachment
     * @param attachmentID: unique id for this attachment
     * @return status of delete operation performed on attachment corresponding to this attachment ID
     * @throws FormsPortalException
     */
    public boolean deleteAttachment (String attachmentID) throws FormsPortalException;

    /**
     * To get attachment bytes
     * @param attachmentID: unique id for this attachment
     * @return data corresponding to this attachmentID
     * @throws FormsPortalException
     */
    public byte[] getAttachment (String attachmentID) throws FormsPortalException;
}
```

>[!NOTE]
>
>草稿ID字段长度的最小值为26个字符。 Adobe建议将草稿ID长度设置为26个或更多字符。

## 提交数据服务{#submission-data-service}

要自定义提交用户数据的存储，您需要实施`SubmitDataService`界面的所有方法。 以下示例代码介绍了方法和参数。

```java
/**
 * SubmitDataService service will get/delete/submit user data (attachments and form data) filled with a submission of Form
 */
public interface SubmitDataService {

    /**
     * Submits the user data passed in argument map
     * @param userDataID, unique identifier associated with this user data
     * @param formName, name of the form whose draft is being submitted
     * @param formData, user data associated with this submission
     * @return userdataID, corresponding to which the user data has been stored and which can be used later to retrieve this data
     * @throws FormsPortalException
     */
    public String saveData (String userDataID, String formName, String formData) throws FormsPortalException;

    /**
     * Submits the user data provided as byte array
     * @param id
     * @param data
     * @return id corresponding to saved data
     * @throws FormsPortalException
     */
    public String saveData (String id, byte[] data) throws FormsPortalException;

    /** Submits the user data provided as byte array asynchronously for the user name provided in the options map
     * @param data data to be saved in bytes
     * @param options map containing options that affect this save
     * @return id of the saved data instance
     */
    public String saveDataAsynchronusly(byte[] data, Map<String, Object> options) throws FormsPortalException;

    /**
     * Gets the user data stored against the ID passed as argument
     * @param userDataID: unique id associated with this user data for this submission
     * @return user data associated with this submission
     * @throws FormsPortalException
     */
    public byte[] getData(String userDataID) throws FormsPortalException;

    /**
     * Deletes user data stored against the userDataID
     * @param userDataID: unique id associated with this user data for this submission
     * @return status of the delete operation on this submission
     * @throws FormsPortalException
     */

    public boolean deleteData(String userDataID) throws FormsPortalException;

    /**
     * Submits the attachment bytes passed as argument
     * @param attachmentsBytes: would expect byte array of the attachment for this submission
     * @return attachmentID for the attachment just saved (so that it could be retrieved later)
     * @throws FormsPortalException
     */
    public String saveAttachment(byte[] attachmentBytes) throws FormsPortalException;

    /** Submits the attachment bytes passed as argument asynchronously for the user id provided in options map.
     * @param attachmentBytes would expect byte array of the attachment for this submission
     * @param options map containing options that affect this save
     * @return attachmentID for the attachment just saved (so that it could be retrieved later)
     * @throws FormsPortalException
     */
    public String saveAttachmentAsynchronously(byte[] attachmentBytes, Map<String, Object> options) throws FormsPortalException;

    /**
     * To delete an attachment
     * @param attachmentID: Unique id for this attachment
     * @return status of delete operation performed on attachment corresponding to this attachment ID
     * @throws FormsPortalException
     */
    public boolean deleteAttachment (String attachmentID) throws FormsPortalException;

    /**
     * To get attachment bytes
     * @param attachmentID: unique id for this attachment
     * @return data corresponding to this attachmentID
     * @throws FormsPortalException
     */
    public byte[] getAttachment (String attachmentID) throws FormsPortalException;
}
```

Forms Portal使用通用唯一标识符(UUID)概念为每个草稿和提交的表单生成唯一ID。 您还可以生成您自己的唯一ID。 您可以实施接口FPKeyGeneratorService、覆盖其方法并开发自定义逻辑，以便为每个草稿和提交的表单生成自定义唯一ID。 此外，将自定义ID生成实施的服务排名设置为大于0。 它可确保使用自定义实施，而不是默认实施。

```java
public interface FPKeyGeneratorService {
    /**
     * returns a unique id for draft and submission
     *
     * @param none
     * @return unique id in string format as per the implementation
     * @throws FormsPortalException
     */
    public String getUniqueId() throws FormsPortalException;
}
```

您可以使用以下注释来增加通过上述代码生成的自定义ID的服务排名：

`@Properties(value = { @Property(name = "service.ranking", intValue = 15) } )`

要使用上述注释，请将以下内容导入您的项目：

```java
import org.apache.felix.scr.annotations.Properties;
import org.apache.felix.scr.annotations.Property;
```
