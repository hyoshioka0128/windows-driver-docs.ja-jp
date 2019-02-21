---
title: TxtSetup.oem ファイルのディスク セクション
description: あるディスク セクションでは、デバイスのインストール キット内のディスクを識別します。
ms.assetid: 0a1c0bf1-b4b9-45bc-af48-26f19bc72061
keywords:
- ディスクのセクションの TxtSetup.oem ファイルのデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- Disks Section of a TxtSetup.oem File
api_type:
- NA
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: d7cec3698511bae82b4047404dcf2fe63f1ff236
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529157"
---
# <a name="disks-section-of-a-txtsetupoem-file"></a>TxtSetup.oem ファイルのディスク セクション


**ディスク**セクションは、デバイスのインストール キット内のディスクを識別します。 このセクションでは、次の形式があります。

``` syntax
[Disks]
diskN = "description",tagfile,directory
...
```

<a href="" id="diskn"></a>*diskN*  
後続のセクションで、ディスクを識別するために使用できるキーを指定します。

<a href="" id="description"></a>*説明*  
ディスクの名前を含む文字列を指定します。 Windows では、説明を使用して、ディスクを挿入するユーザーに確認します。

<a href="" id="tagfile"></a>*tagfile*  
ディスク上の検証ファイルの名前を指定します。 ファイル名は、ルートから完全なパスとして指定する必要があり、ドライブを指定する必要があります。 Windows は、ユーザーに適切なディスクが挿入されていることを確認するには、このファイルをチェックします。

<a href="" id="directory"></a>*ディレクトリ*  
インストール ファイルが配置されるディスク上のディレクトリを指定します。 ディレクトリのルートから完全なパスとして指定する必要があり、ドライブを指定する必要があります。

次の例は、**ディスク**セクションの 2 つのディスク、インストール キット。

``` syntax
[Disks]
disk1 = "OEM SCSI driver disk 1",\disk1.tag,\
disk2 = "OEM SCSI driver disk 2",\disk2.tag,\
; ...
```

 

 





