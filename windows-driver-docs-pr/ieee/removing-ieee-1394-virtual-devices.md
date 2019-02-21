---
title: IEEE 1394 の仮想デバイスの削除
description: IEEE 1394 の仮想デバイスの削除
ms.assetid: ea2d4b9e-7774-42dc-98dd-d95298012d72
keywords:
- エミュレーション ドライバー WDK IEEE 1394 バス
- ハードウェア エミュレーション ドライバー WDK IEEE 1394 バス
- 仮想デバイス WDK IEEE 1394 バス
- 仮想デバイスを削除します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3f37fcbd77653fcc4e0b7b34931265a595758766
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552201"
---
# <a name="removing-ieee-1394-virtual-devices"></a>IEEE 1394 の仮想デバイスの削除





これには 2 つの仮想デバイスの物理デバイス オブジェクト (PDO) を削除する方法があります。

1.  **標準、プラグ アンド プレイ (PnP) デバイスを削除する方法**します。 このメソッドを使用して、送信には、ドライバーがある、 [ **IRP\_MN\_削除\_デバイス**](https://msdn.microsoft.com/library/windows/hardware/ff551738)仮想デバイスに要求します。

    I/O スタックは、次の値を含める必要があります。

    -   **MajorFunction** IRP を =\_MJ\_PNP
    -   **MinorFunction** IRP を =\_MN\_削除\_デバイス

2.  **型の I/O 要求パケット (IRP)** IOCTL\_IEEE1394\_API\_要求。このメソッドを使用して、送信には、ドライバーがある、 [ **IRP\_MJ\_デバイス\_コントロール**](https://msdn.microsoft.com/library/windows/hardware/ff550744)仮想デバイスに要求します。

    I/O スタックは、次の値を含める必要があります。

    -   **MajorFunction** IRP を =\_MJ\_デバイス\_コントロール
    -   **Parameters.DeviceIoControl.IoControlCode** = [**IOCTL\_IEEE1394\_API\_REQUEST**](https://msdn.microsoft.com/library/windows/hardware/ff537241)

    IRP では、次の値を含める必要があります。

    -   **AssocicatedIrp.SystemBuffer -&gt;SystemBuffer**を指す、 [ **IEEE1394\_API\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff537204)構造体
    -   **RequestNumber** IEEE1394 のメンバー\_API\_要求 = [ **IEEE1394\_API\_削除\_仮想\_デバイス**](https://msdn.microsoft.com/library/windows/hardware/ff537201)

最初のメソッド (IRP\_MN\_削除\_デバイス)、デバイスが削除されますが、次回、コンピューターが開始を復元、デバイスが永続的な場合。 2 番目のメソッド (IEEE1394\_API\_削除\_仮想\_デバイス) が不要になったリブート持続するように、デバイスを完全に削除されます。 次回のコンピューターの起動時、デバイスは復元されません。

仮想デバイスが存在する通常の PnP メカニズムにより、上位レベルのドライバーまたはユーザー モードのサービスを確認できることに注意してください。 この機構は、仮想のドライバーの INF ファイルで提供されている GUID クラスを使用します。

 

 




