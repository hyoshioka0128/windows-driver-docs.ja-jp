---
title: ネットワーク INF ファイル内の DDInstall.Services セクション
description: ネットワーク INF ファイル内の DDInstall.Services セクション
ms.assetid: 5d5cc0ac-fbe2-4791-9c74-fdf9906faff6
keywords:
- INF ファイルの WDK ネットワーク、DDInstall.Services セクション
- ネットワーク INF ファイル、WDK DDInstall.Services セクション
- DDInstall.Services セクション WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6fcd4f1039b3698db0430704d21dcd90017f4c20
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354615"
---
# <a name="ddinstallservices-section-in-a-network-inf-file"></a>ネットワーク INF ファイル内の DDInstall.Services セクション





A *DDInstall*.**サービス**ネットワーク INF ファイルのセクションは、ジェネリックに基づきます[ **INF DDInstall.Services セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-services-section)します。

A *DDInstall*.**サービス**セクションは、1 つ以上含まれています**AddService** 、INF-ライター定義の参照ディレクティブ*サービス-インストール セクション*方法とタイミングを指定する、。サービスの特定のコンポーネントのドライバーが読み込まれます。

A *DDInstall*.**サービス**Net コンポーネント (アダプター) をインストールする INF ファイルでセクションが必要ですオプションをインストールする INF ファイルでは、 **NetTrans**、 **NetClient**、または **。NetService**コンポーネント。

**注**  **NetClient**コンポーネントは Windows 8.1、Windows Server 2012 R2 で非推奨以降。

 

**AddService**ディレクティブで、 *DDInstall*.**サービス**セクションを参照できます、*エラー ログ-インストール セクション*コンポーネントのエラー ログをインストールします。 エラー ログでは、すべてのネットワーク コンポーネントの省略可能です。

詳細については、次を参照してください。 [ **INF AddService ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addservice-directive)します。

例を次に、 *DDInstall*.**サービス** セクションで、*サービス-インストール セクション*、*エラー ログ-インストール セクション*、および*追加レジストリ セクション*によって参照されます。**AddReg**ディレクティブで、*エラー ログ-インストール セクション*:

```cpp
[a1.ndi.NT.Services]
AddService = a1, 2, a1.AddService, a1.AddEventLog
 
[a1.AddService]
DisplayName = %Adapter1.DispName%
ServiceType = 1 ;SERVICE_KERNEL_DRIVER
StartType = 2 ;SERVICE_AUTO_START
ErrorControl = 1 ;SERVICE_ERROR_NORMAL
ServiceBinary = %12%\a1.sys
LoadOrderGroup = NDIS
 
[a1.AddEventLog]
AddReg = a1.AddEventLog.reg
 
[a1.AddEventLog.reg]
HKR,,EventMessageFile,0x00020000,"%%SystemRoot%%\System32\netevent.dll"
HKR,,TypesSupported,0x00010001,7
```

*ServiceName*のパラメーター、 **AddService**ディレクティブであり、上記の例では**a1**(最初の**AddService**パラメーター)、コンポーネントに一致する必要があります**Ndi\\サービス**値。 詳細については、次を参照してください。 [Ndi キーに値を Adding Service-Related](adding-service-related-values-to-the-ndi-key.md)します。

 

 





