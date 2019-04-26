---
title: NTSTATUS 値の使用
description: NTSTATUS 値の使用
ms.assetid: fe823930-e3ff-4c95-a640-bb6470c95d1d
keywords:
- NTSTATUS 値 WDK カーネル
- ドライバー サポート ルーチン WDK カーネル
- 戻り値の WDK カーネル
- WDK NTSTATUS 値の戻り値のテスト
- 成功した場合は、WDK NTSTATUS 値を値します。
- WDK NTSTATUS 値情報の値
- 警告 WDK NTSTATUS 値
- エラー値 WDK NTSTATUS 値します。
- 状態情報の WDK NTSTATUS 値
- 戻り値のチェック
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 57935e7980e5aef8a571bbc9b80e26bf841bb879
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354202"
---
# <a name="using-ntstatus-values"></a>NTSTATUS 値の使用





多くのカーネル モード[標準ドライバー ルーチン](https://docs.microsoft.com/windows-hardware/drivers/kernel/introduction-to-standard-driver-routines)と[ドライバー サポート ルーチン](https://msdn.microsoft.com/library/windows/hardware/ff563889)戻り値の NTSTATUS 型を使用します。 さらに、ドライバーは IRP の NTSTATUS 型の値を提供[ **IO\_状態\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/ff550671)ときに構造体[Irp の完了](completing-irps.md)します。 NTSTATUS 型は Ntdef.h で定義され、システム提供の状態コードは Ntstatus.h に定義されています。 (ベンダーも定義できますプライベート ステータス コードをする必要はほとんどありませんが。 詳細については、次を参照してください[新しい NTSTATUS の値を定義する](defining-new-ntstatus-values.md)。)。

NTSTATUS 値は 4 種類に分けられます。 成功を示す値、値の情報、警告、およびエラーの値。

さまざまな値は、それぞれの種類に割り当てられます。 正常に返された、ルーチンからのテストするときによくある間違いは、ステータスのルーチンの戻り値を比較する\_成功します。 この比較は、いくつかの成功を示す値の 1 つだけをチェックします。

戻り値をテストする場合は、(Ntdef.h で定義されている) 次、システム提供のマクロのいずれかを使用する必要があります。

<a href="" id="nt-success-status-"></a>NT\_成功 (*状態*)  
評価される**TRUE**で戻り値が指定されている場合*状態*成功型 (− 0x3FFFFFFF 0) か、情報の種類 (0x40000000 − 0x7FFFFFFF)。

<a href="" id="nt-information-status-"></a>NT\_情報 (*状態*)  
評価される**TRUE**で戻り値が指定されている場合*状態*情報の種類 (0x40000000 − 0x7FFFFFFF)。

<a href="" id="nt-warning-status-"></a>NT\_警告 (*状態*)  
評価される**TRUE**で戻り値が指定されている場合*状態*は警告の種類 (0x80000000 − 0xBFFFFFFF)。

<a href="" id="nt-error-status-"></a>NT\_エラー (*状態*)  
評価される**TRUE**で戻り値が指定されている場合*状態*はエラーの種類 (0xC0000000 - 0 xffffffff) です。

たとえば、ドライバーを呼び出す[ **IoRegisterDeviceInterface** ](https://msdn.microsoft.com/library/windows/hardware/ff549506)デバイス インターフェイスを登録します。 かどうか、ドライバーは、NT を使用して、戻り値を確認します\_成功のマクロにマクロを評価する**TRUE**ルーチンに状態が返された場合\_成功すると、エラーがないことを示します、情報が返された場合、または。状態\_オブジェクト\_名前\_EXISTS で、デバイスのインターフェイスが既に登録されていることを示します。

別の例として、たとえば、ドライバーは呼び出し[ **ZwEnumerateKey** ](https://msdn.microsoft.com/library/windows/hardware/ff566447)を指定したレジストリ キーのサブキーを列挙します。 場合、NT\_成功マクロに評価されます**FALSE**、ルーチンに状態が返される可能性があります\_無効な\_パラメーター、エラー コード、ルーチンにの状態が返されるため、または\_いいえ\_詳細\_エントリで、警告コードです。

最後の例では、ドライバーは IRP をデバイスから情報を読み取る低レベルのドライバーが原因となるを送信するとします。 下位レベルのドライバーが状態を返すことによって応答可能性があります、要求元のドライバー バッファーが小さすぎてすべての情報が表示される場合、\_バッファー\_すぎます\_小規模で、エラー コードします。 下位レベルのドライバーが応答可能なデータを指定し、状態を返すことで最初のドライバーが、いくつか受け取ることができるバッファーを指定する場合は、すべてではなく、要求された情報の\_バッファー\_オーバーフローの場合、これは、警告コード。 最初のドライバーが NT を使用して状態の値をテストする場合\_成功または NT\_エラー正しく、可能性がありますが誤って削除しない、受信した情報の一部です。

 

 




