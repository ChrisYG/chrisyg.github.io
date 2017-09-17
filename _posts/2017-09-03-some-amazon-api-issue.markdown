---
layout: post
title: "Some reasons for errors in python amazon simple product api"
date:   2017-09-03 20:00:00 -0700
categories: Django
---
Recently I found the ASPC's link for uploading multiple books was not working. Internally we used a python wrapper for the Amazon Product Advertising API, which is open-source in GitHub: https://github.com/yoavaviram/python-amazon-simple-product-api.

Initially I thought, like most people, we had a "400 : Bad Request" error, which was discussed and had a solution here: https://github.com/yoavaviram/python-amazon-simple-product-api/issues/110.

But I found our actual error was 403 unauthorized. So if anyone happens to have this error too, it's because either you don't have a user in Amazon IAM, or, more likely, which is my case, your user owning the access key doesn't have permission to call the product advertising API.
