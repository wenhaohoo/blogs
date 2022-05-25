---
title: search功能的实现
date: 2022-05-15
description: search功能的实现
tag: conponent
author: holobo
---

# searchs

## 先加入input和button组件，样式随意组合

## 1、设置state监听input输入的onchange

## 2、在button上开启onclick事件获取oninput的输入内容
```
export const SearchPosts = async (q) => {
  const query = querystring.stringify({ q })
  return await axios({
    method: 'GET'
    url: '/api/search?' + query
})
const handleSearch = async (value) => {
  const posts = await SearchPosts(value)
  setPosts(posts.data)
}
```
## 3、建立api接口search.js，发送请求
_参数包含请求req和响应res，req为url后面query部分，亦为搜索关键字_
 _res返回status，也就是返回响应代码，200为success，400为error_
 _随后filter对其进行遍历，将所有q用tolowercase将大小写的区分去除_
 _并将psot__需要的json取出存放至最后返回包含lq的搜索结果_

### 请求内容：
```

export default function handler(req, res) {
  const { q } = req.query
  if (!q) {
    res.status(400).json({ error: 'q is required for searching posts' })
  } else {
    const postList = json.posts
    const filteredPost = postList.filter(post => {
      const lq = q.toLowerCase()
      const { title, description = '', content = '' } = post
      return title.toLowerCase().includes(lq) || description.toLowerCase().includes(lq) || content.toLowerCase().includes(lq)
    })
    filteredPost.forEach(p => delete p.content)
    res.status(200).json(filteredPost)
  }
}

```
 

