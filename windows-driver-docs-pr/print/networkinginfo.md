---
title: NetworkingInfo
description: NetworkingInfo
ms.assetid: 81c615d4-8a7c-4d28-a3ce-5233899e35cf
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: cba60c6300cfb3c745028c51bc078bbb6a53f777
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346548"
---
# <a name="networkinginfo"></a>NetworkingInfo


スキーマのパス:\\Printer.DeviceInfo:NetworkingInfo

ノード型: プロパティ

このセクションでは、全体として、デバイスに関連付けられているデータについて説明します。 ユーザーまたは管理者は、自分のデバイスを個人用に設定するには、このデータの多くで設定できます。

NetworkingInfo では、2 つの値があります。**ホスト名**と**IPAddress**します。

### <a name="span-idhostnamespanspan-idhostnamespan-hostname"></a><span id="hostname"></span><span id="HOSTNAME"></span> ホスト名

スキーマのパス:\\Printer.DeviceInfo:NetworkingInfo.HostName

ノード型: 値

データ型: BIDI\_文字列

現在のネットワーク デバイスのホスト名を含む説明: A 文字列。 この情報は、すべてのデバイスのできない可能性があります。

### <a name="span-idipaddressspanspan-idipaddressspan-ipaddress"></a><span id="ipaddress"></span><span id="IPADDRESS"></span> IPAddress

スキーマのパス:\\Printer.DeviceInfo:NetworkingInfo.IPAddress

ノード型: 値

データ型: BIDI\_文字列

デバイスの現在の TCP/IP アドレスを格納して description: A 文字列。 このアドレスは、IPV4 または IPV6 のいずれかの形式である可能性があります。 このアドレスは、印刷デバイスとの通信にポート モニタが現在使用されているアドレスです。

 

 




