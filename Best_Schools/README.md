# Best_Schools

### Category

Web

### Description

An anonymous company has decided to publish a ranking of the best schools, and it is based on the number of clicks on a button! Make sure you get the 'Flag CyberSecurity School' in first place and you'll get your reward!
<br><br>
Format : **Hero{flag}**<br>
Author : **Dat**

### Write Up

server.js

```
const middleware_rate_limit = (req,res,next) => {
  if(req.originalUrl === "/graphql")
  {
    var query = "";
    try{
      req.body.map(function(item){query += item['query'].toString();})
    }catch(err)
    {
      query = req.body.query
    }
    if(query.includes("increaseClickSchool"))
    {
      if(!clients.hasOwnProperty(req.socket.remoteAddress))
      {
        clients[req.socket.remoteAddress] = -1
      }
        if(parseInt((Date.now() - clients[req.socket.remoteAddress])/1000) > 60 )
        {
          clients[req.socket.remoteAddress] = Date.now();
          next()
        }
        else
        {
          res.status(429).json({"code":429,"error":"You're going too fast !"})
        }
    }
    else
    {
      next();
    }
  }
  else
  {
    next();
  }
}
```

When you click Action : Im’ at this school you must wait 1 minute to continue clicking it twice for any school.

### Endpoint

GraphQL services often use similar endpoint suffixes and in this challenge has at less  2 endpoints: <b>/graphql, /graphql/graphql</b>

### Attack

I realized when I set Post  <b>/graphql/graphql</b> I can send it with no limit time. 

![example](/Best_Schools/image_wirteup/image1.png)

I will set tenth time increaseClickSchool so I need only several times to make number click of Flag CyberSecurity School more than 1337

![example](/Best_Schools/image_wirteup/image2.png)


### Flag

![flag](/Best_Schools/image_wirteup/image3.png)

Hero{gr4phql_b4tch1ng_t0_byp4ss_r4t3_l1m1t_!!}