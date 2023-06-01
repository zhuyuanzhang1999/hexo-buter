---
title: images in GitHub
tags:
  - GitHub
  - images
id: '459'
categories:
  - - GitHub
date: 2023-03-17 21:00:00
---

### insert images in GitHub


一种常用的方法是使用GitHub的issue功能来上传图片，然后复制图片的URL，在Markdown文件中使用![]()语法来引用图片。具体步骤如下：

- 在你的仓库中创建一个新的issue，可以命名为Images或其他任意名称。
- 将你想要上传的图片拖拽到评论框中，或者点击selecting them来选择本地文件。
- 等待图片上传完成，你会看到评论框中出现类似![](https://user-images.githubusercontent.com/...)的语句。
- 复制这个语句，粘贴到你想要放入图片的Markdown文件中，例如README.md。
- 保存并提交你的修改，然后在GitHub上查看效果。

注意：如果你不想让别人看到你创建的issue，可以将其关闭或删除。如果你不想让别人收到关于这个issue的通知邮件，可以批量上传多张图片后再保存或关闭issue。如果你想给图片添加标题或替代文本（alt text），可以在方括号[]中输入文字。
###
  Diagram
    USER ||--|| BLOGGER : 一对一
    BLOGGER ||--|{ PHOTO : 一对多
    BLOGGER ||--|{ MESSAGE : 一对多
    USER ||--|{ MESSAGE : 一对多
    BLOGGER ||--|{ ARTICLE : 一对多
    ARTICLE }|--|| CATEGORY : 多对一
    ARTICLE }|..|{ TAG : 多对多
    ARTICLE ||--|{ COMMENT : 一对多
    USER ||--|{ COMMENT : 一对多

    USER {
        user_id 主属性
        username 属性
        password 属性
        email 属性
        phone 属性
    }

    BLOGGER {
        blogger_id 主属性
        nickname 属性
        bio 属性
        avatar 属性
    }

    PHOTO {
        photo_id 主属性
        url 属性
        caption 属性
        upload_time 属性
    }

    MESSAGE {
        message_id 主属性
        content 属性
        send_time 属性
    }

    ARTICLE {
        id 主属性
        title 属性
        content 属性
        publish_time 属性
        view_count 属性
    }

    CATEGORY {
        id 主属性
        name 属性
    }

    TAG {
        id 主属性
        name 属性
    }

    COMMENT {
        comment_id 主属性
        content 属性
        reply_to 属性
        post_time 属性
    }



