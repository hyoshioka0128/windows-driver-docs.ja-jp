---
title: NTSTATUS 値の使用
description: NTSTATUS 値の使用
ms.assetid: fe823930-e3ff-4c95-a640-bb6470c95d1d
keywords:
- NTSTATUS 値 WDK カーネル
- ドライバーサポートルーチン WDK カーネル
- 戻り値 WDK カーネル
- 戻り値のテスト WDK NTSTATUS 値
- 成功値 WDK NTSTATUS 値
- 情報値 WDK NTSTATUS 値
- 警告 WDK NTSTATUS 値
- エラー値 WDK NTSTATUS 値
- ステータス情報 WDK NTSTATUS 値
- チェック (戻り値を)
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 15ea1f813b60532a140e1dfd1001d24b2e35afa5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838345"
---
# <a name="using-ntstatus-values"></a>NTSTATUS 値の使用





カーネルモードの[標準ドライバールーチン](https://docs.microsoft.com/windows-hardware/drivers/kernel/introduction-to-standard-driver-routines)と[ドライバーサポートルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)の多くは、戻り値には NTSTATUS 型を使用します。 また、 [irp の完了](completing-irps.md)時に、ドライバーは、Irp の[**IO\_ステータス\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)構造に、NTSTATUS で型指定された値を提供します。 NTSTATUS の種類は Ntdef に定義されており、システムによって提供される状態コードは、Ntstatus に定義されています。 (ベンダーは、プライベートステータスコードを定義することもできますが、必要になることはほとんどありません。 詳細については、「[新しい NTSTATUS 値の定義](defining-new-ntstatus-values.md)」を参照してください。

NTSTATUS 値は、成功値、情報値、警告、およびエラー値の4種類に分類されます。

型ごとに多数の値が割り当てられます。 ルーチンから正常に返されたことをテストする場合の一般的な誤りは、ルーチンの戻り値と状態\_SUCCESS を比較することです。 この比較では、成功値のうちの1つだけがチェックされます。

戻り値をテストする場合は、次のシステム指定マクロのいずれかを使用する必要があります (Ntdef. h で定義)。

<a href="" id="nt-success-status-"></a>NT\_成功 (*状態*)  
*Status*によって指定された戻り値が成功の型 (0 − 0x3FFFFFFF) または情報の種類 (0X40000000 − 0x7fffffff) である場合は、 **TRUE**に評価されます。

<a href="" id="nt-information-status-"></a>NT\_情報 (*状態*)  
*Status*によって指定された戻り値が情報型 (0X40000000 − 0x7fffffff) である場合、 **TRUE**に評価されます。

<a href="" id="nt-warning-status-"></a>NT\_警告 (*状態*)  
*Status*によって指定された戻り値が警告の種類 (0X80000000 − 0xBFFFFFFF) の場合、 **TRUE**に評価されます。

<a href="" id="nt-error-status-"></a>NT\_エラー (*状態*)  
*Status*によって指定された戻り値がエラーの種類 (0XC0000000-0xffffffff) である場合、 **TRUE**に評価されます。

たとえば、ドライバーが[**IoRegisterDeviceInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterdeviceinterface)を呼び出してデバイスインターフェイスを登録するとします。 ドライバーが NT\_SUCCESS マクロを使用して戻り値をチェックした場合、ルーチンが SUCCESS\_STATUS を返した場合、エラーがないこと、または情報ステータスステータス\_オブジェクトが返された場合、マクロは**TRUE**と評価され @no__tデバイスインターフェイスが既に登録されていることを示す 4_ NAME\_EXISTS (_s)\_

別の例として、ドライバーが[**ZwEnumerateKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwenumeratekey)を呼び出して、指定されたレジストリキーのサブキーを列挙するとします。 NT\_SUCCESS マクロが**FALSE**と評価された場合、ルーチンがステータス\_無効な\_パラメーターを返したか、エラーコードであるか、またはルーチンが\_status を返して\_のエントリがそれ以上\_ないことが原因である可能性があります。これは警告コードです。

最後の例として、ドライバーが IRP を送信して、下位レベルのドライバーがデバイスから情報を読み取るとします。 要求元のドライバーによって、情報を受信するには小さすぎるバッファーが指定されている場合、下位レベルのドライバーは、ステータス\_バッファー\_(エラーコード) が小さい\_を返すことによって応答する可能性があります。 最初のドライバーが、要求された情報の一部ではなく一部を受け取ることができるバッファーを指定した場合、下位レベルのドライバーは、できるだけ多くのデータを提供してから、ステータス\_バッファー\_オーバーフロー (警告コード) を返すことで応答する可能性があります。 最初のドライバーが NT\_SUCCESS または NT\_エラーを使用して状態の値をテストした場合、受信した情報の一部が誤って破棄される可能性があることに注意してください。

 

 




