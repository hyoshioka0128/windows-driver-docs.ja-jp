---
title: Bluetooth HFP DDI Ioctl
description: Windows 8 では、Bluetooth バイパス オーディオ接続の動作に、ハンズフリー プロファイル (HFP) クラス ドライバーを使用するオーディオ ドライバーを許可する DDI の一部として一連の I/O 制御コード (Ioctl) について説明します。
ms.assetid: 94B6F113-5130-4772-B8A0-5C9992501824
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ae729e5e7f8ef4ab4372f66b342eb85ad065957f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558899"
---
# <a name="bluetooth-hfp-ddi-ioctls"></a>Bluetooth HFP DDI Ioctl


Windows 8 では、Bluetooth バイパス オーディオ接続の動作に、ハンズフリー プロファイル (HFP) クラス ドライバーを使用するオーディオ ドライバーを許可する DDI の一部として一連の I/O 制御コード (Ioctl) について説明します。

特に記載がない限り、次に示します。 このセクションでは、すべての Ioctl の場合は true。

-   要求が成功した場合、状態の情報メンバー\_ブロック構造が出力バッファーのバイト単位のサイズに設定されています。 それ以外の場合、情報メンバーは、0 に設定されます。 状態のメンバーは、NTSTATUS 値に設定されます。

-   すべての IOCTL に必要な IRQL &lt;= パッシブ\_レベル。

-   オーディオ ドライバーは IRP に Ioctl を使用する必要があります\_MJ\_デバイス\_コントロール要求。

IOCTL 関数コードのほとんどは、オーディオ ドライバーが、io FileObject ポインターを初期化する必要があります\_スタック\_HFP ドライバー、オーディオ ドライバーは IRP HFP ドライバーに送信するようにデバイスの制御を初期化するときの場所。 通常、オーディオ ドライバーは、IoGetDeviceObjectPointer を呼び出すことによって、ファイル オブジェクト ポインターを取得します。

オーディオ ドライバーは任意のスレッド (つまり、「非同期」の要求) でこれらの要求の多くに送信します。 このような場合は、オーディオ ドライバーは IRP IoAllocateIrp メソッドを使用して自身をビルドして、呼び出し元 IoBuildDeviceIoControlRequest ではなく、直接 IRP のフィールドを設定する必要があります。

これらの Windows 8 Ioctl の詳細については、以下のトピックです。

[**IOCTL\_BTHHFP\_DEVICE\_GET\_DESCRIPTOR**](https://msdn.microsoft.com/library/windows/hardware/dn265108)

[**IOCTL\_BTHHFP\_DEVICE\_GET\_VOLUMEPROPERTYVALUES**](https://msdn.microsoft.com/library/windows/hardware/dn265113)

[**IOCTL\_BTHHFP\_DEVICE\_GET\_KSNODETYPES**](https://msdn.microsoft.com/library/windows/hardware/dn265110)

[**IOCTL\_BTHHFP\_DEVICE\_GET\_CONTAINERID**](https://msdn.microsoft.com/library/windows/hardware/dn265107)

[**IOCTL\_BTHHFP\_DEVICE\_REQUEST\_CONNECT**](https://msdn.microsoft.com/library/windows/hardware/dn265114)

[**IOCTL\_BTHHFP\_デバイス\_要求\_切断**](https://msdn.microsoft.com/library/windows/hardware/dn265115)

[**IOCTL\_BTHHFP\_DEVICE\_GET\_CONNECTION\_STATUS\_UPDATE**](https://msdn.microsoft.com/library/windows/hardware/dn265106)

[**IOCTL\_BTHHFP\_スピーカー\_設定\_ボリューム**](https://msdn.microsoft.com/library/windows/hardware/dn265119)

[**IOCTL\_BTHHFP\_SPEAKER\_GET\_VOLUME\_STATUS\_UPDATE**](https://msdn.microsoft.com/library/windows/hardware/dn265118)

[**IOCTL\_BTHHFP\_MIC\_SET\_VOLUME**](https://msdn.microsoft.com/library/windows/hardware/dn265117)

[**IOCTL\_BTHHFP\_MIC\_GET\_VOLUME\_STATUS\_UPDATE**](https://msdn.microsoft.com/library/windows/hardware/dn265116)

[**IOCTL\_BTHHFP\_STREAM\_OPEN**](https://msdn.microsoft.com/library/windows/hardware/dn265122)

[**IOCTL\_BTHHFP\_STREAM\_CLOSE**](https://msdn.microsoft.com/library/windows/hardware/dn265120)

[**IOCTL\_BTHHFP\_STREAM\_GET\_STATUS\_UPDATE**](https://msdn.microsoft.com/library/windows/hardware/dn265121)

Windows 8.1 では、Ioctl のセットを次の新しいものを追加することで更新します。

[**IOCTL\_BTHHFP\_DEVICE\_GET\_DESCRIPTOR2**](https://msdn.microsoft.com/library/windows/hardware/dn265109)

[**IOCTL\_BTHHFP\_DEVICE\_GET\_NRECDISABLE\_STATUS\_UPDATE**](https://msdn.microsoft.com/library/windows/hardware/dn265112)

Windows 10 では、次の新しいサブスクリプションを追加して Ioctl のセットが更新します。

[**IOCTL\_BTHHFP\_DEVICE\_GET\_CODEC\_ID**](https://msdn.microsoft.com/library/windows/hardware/dn798965)

これらの Ioctl で動作する構造については、[Bluetooth HFP DDI 構造](bluetooth-hfp-ddi-structures.md)を参照してください。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[Bluetooth HFP DDI 構造体](bluetooth-hfp-ddi-structures.md)

 

 






