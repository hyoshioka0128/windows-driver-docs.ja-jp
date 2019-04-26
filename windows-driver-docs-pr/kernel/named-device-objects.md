---
title: 名前付きデバイス オブジェクト
description: 名前付きデバイス オブジェクト
ms.assetid: 4e24f0c1-57b2-4e06-a7f5-9a93d365ac8c
keywords:
- という名前のデバイス オブジェクトの WDK カーネル
- 名前付きのデバイス オブジェクトの WDK カーネル
ms.date: 09/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2bb7c6f5ce76485b5715fb5b5a9a7c8de02ca4b7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341958"
---
# <a name="named-device-objects"></a>名前付きデバイス オブジェクト





すべてのオブジェクトの manager のオブジェクトと同様に、デバイス オブジェクトは、という名前または名前のないことができます。 ユーザー モード アプリケーションが I/O 要求を行うと、名前で、操作の対象を指定します。 オブジェクト マネージャーは、I/O 要求の送信先を決定する名前を解決します。

> [!IMPORTANT]
> ドライバーのセキュリティ名前デバイス オブジェクトに必要な場合にのみを強化します。 名前付きのデバイス オブジェクトは、一般にのみ例については、旧システムのために必要な特定の名前を使用してデバイスを開くことが必要とするアプリケーションがある場合、または非 PNP デバイス/制御デバイスを使用している場合。  WDF のドライバーがという名前の PnP デバイスを使用して、シンボリック リンクを作成するためにする必要がないことに注意してください[WdfDeviceCreateSymbolicLink](https://msdn.microsoft.com/library/windows/hardware/ff545939.aspx)します。

呼び出すときに、ドライバーはデバイス オブジェクトの名前を指定できます[ **IoCreateDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff548397)または[ **IoCreateDeviceSecure** ](https://msdn.microsoft.com/library/windows/hardware/ff548407)デバイスを作成するにはオブジェクト。 詳細とデバイス オブジェクトの名前を付ける方法については、次を参照してください。 [NT デバイス名](nt-device-names.md)します。
  
名前付きのデバイス オブジェクトは、シンボルは、MS-DOS デバイス名を持つことができますもによって作成されたリンク[ **IoCreateSymbolicLink** ](https://msdn.microsoft.com/library/windows/hardware/ff549043)または[ **IoCreateUnprotectedSymbolicLink**](https://msdn.microsoft.com/library/windows/hardware/ff549050). WDM ドライバー、MS-DOS デバイス名は通常必要ありません。 詳細については、次を参照してください。 [MS-DOS デバイス名](ms-dos-device-names.md)します。

> [!IMPORTANT]
> 名前付きのデバイス オブジェクトを使用する場合は、使用[IoCreateDeviceSecure](https://msdn.microsoft.com/library/windows/hardware/ff548407.aspx)し、それをセキュリティ保護するための SDDL を指定します。 実装に[IoCreateDeviceSecure](https://msdn.microsoft.com/library/windows/hardware/ff548407.aspx) DeviceClassGuid を常にカスタム クラス GUID を指定します。 既存のクラス GUID は、ここを指定する必要があります。 そうと、セキュリティの設定またはそのクラスに属している他のデバイスの互換性を中断する可能性があります。 詳細については、次を参照してください。 [WdmlibIoCreateDeviceSecure](https://msdn.microsoft.com/library/windows/hardware/mt800803.aspx)します。
> 
> アプリケーションまたはその他の WDF ドライバー、PnP デバイスへのアクセスを許可するためには、デバイスのインターフェイスを使用する必要があります。 詳細については、次を参照してください。[を使用してデバイスのインターフェイス](https://docs.microsoft.com/windows-hardware/drivers/wdf/using-device-interfaces)します。 デバイスのインターフェイスは、デバイス スタックの PDO へのシンボリック リンクとして機能します。 アクセスを制御する方法と、PDO は、INF の SDDL 文字列を指定することです。 INF ファイルの SDDL 文字列でない場合、Windows は既定のセキュリティ記述子を適用します。 詳細については、次を参照してください。[デバイス オブジェクトのセキュリティで保護する](https://docs.microsoft.com/windows-hardware/drivers/kernel/securing-device-objects)と[デバイス オブジェクトの SDDL](https://docs.microsoft.com/windows-hardware/drivers/kernel/sddl-for-device-objects)します。


このセクションには、次のサブセクションが含まれています。

[NT のデバイス名](nt-device-names.md)

[MS-DOS デバイス名](ms-dos-device-names.md)

 

 




