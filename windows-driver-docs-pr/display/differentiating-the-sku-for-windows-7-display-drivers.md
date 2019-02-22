---
title: Windows 7 のディスプレイ ドライバーの SKU を差別化
description: Windows 7 のディスプレイ ドライバーの SKU を差別化
ms.assetid: 3cf72bd5-21bc-4a7f-8c2f-98f8e70d8248
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1222b8231372d251dabb72d6e010dd8aa483b216
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553763"
---
# <a name="differentiating-the-sku-for-windows-7-display-drivers"></a>Windows 7 のディスプレイ ドライバーの SKU を差別化


すべての Windows Server 2008 でのボックスでディスプレイ ドライバーの INF ファイル、Windows Vista SP1、およびそれ以降のバージョンは、ドライバーは、Windows のクライアント エディションのみが、Windows Server Sku でインストールされないことを示す値を含める必要があります。

Windows 7、Windows Vista SP1、Windows Server 2008、および Windows Server 2008 R2、**製造元**ディレクティブの後に、次の形式の文字列でする必要があります。

```inf
NT<platform>...1 
```

この文字列は、プラットフォームは、x86 または amd64 です。

次の例は、**製造元**ディレクティブ、およびそれに続く x86 用のドライバー セクション システム。

```inf
[Manufacturer]
%ATI% = ATI.Mfg,NTx86...1

[ATI.Mfg.NTx86...1]
```

次の例は、**製造元**ディレクティブ、およびそれに続く x64 用のドライバー セクション システム。

```inf
[Manufacturer]
%ATI% = ATI.Mfg,NTamd64...1

[ATI.Mfg.NTamd64...1]
```

詳細については、**製造元**セクションを参照してください[ **INF 製造元セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547454)します。

 

 





