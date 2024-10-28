# Referrrrer

### Category

Web

### Description

Defeated the security of the website which implements authentication based on the [Referer](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Referer) header.

Format : Hero{flag}<br>
Author : Dat

### Files

- [Referrrrer.zip](Referrrrer.zip)

### Write Up

<b>index.js</b>

```
app.get("/admin", (req, res) => {
    if (req.header("referer") === "YOU_SHOUD_NOT_PASS!") {
        return res.send(process.env.FLAG);
    }

    res.send("Wrong header!");
})
```
It said that if I have value of referer is YOU_SHOUD_NOT_PASS!, I will have FLAG

I add Referrer but response is 403

![image](/Referrrrer/image_writeup/image1.png)

<b>nginx.conf</b>

```
location /admin {
    if ($http_referer !~* "^https://admin\.internal\.com") {
        return 403;
    }
        proxy_pass http://express_app;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }
```

<b>index.d.ts</b>

```
* The `Referrer` header field is special-cased,
* both `Referrer` and `Referer` are interchangeable.
```

I see that both Referrer and Referer interchangeable

### Flag

![flag](/Referrrrer/image_writeup/image2.png)

Hero{F4KE_FLAG}