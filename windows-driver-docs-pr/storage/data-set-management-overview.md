---
title: データセット管理 (DSM) の概要
description: '管理アクションは、データセット管理 (DSM) アクションとして、デバイスのデータセット属性に対して実行できます。: "?ASQ'
ms.assetid: cc64c7ad-7d1c-45c7-b236-a43e57086f8d
keywords: ストレージデータセット管理アクション、データセット管理アクション、DSM アクション
ms.localizationpriority: medium
ms.date: 08/23/2019
ms.openlocfilehash: 18590602dc053838890a47455b1449b9fa7aa383
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844575"
---
# <a name="data-set-management-dsm-overview"></a>データセット管理 (DSM) の概要

Windows 7 以降では、ドライバーはデバイスのデータセットに対して管理操作を実行できます。 DSM アクションは Microsoft によって定義されます。

[DEVICE_DSM_ACTION](device-dsm-action-descriptions.md)定数は、アクションを指定します。 この定数は、 [IOCTL_STORAGE_MANAGE_DATA_SET_ATTRIBUTES](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_manage_data_set_attributes)要求のシステムバッファーに格納されている[DEVICE_DSM_INPUT](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ns-ntddstor-_device_manage_data_set_attributes)構造体の**アクション**メンバーで渡されます。 アクションに追加のパラメーターが必要な場合、パラメーターブロックは DEVICE_DSM_INPUT 構造体の直後にあり、 **Parameterblockoffset**は、パラメーターブロックが DEVICE_DSM_INPUT 構造体の先頭からのオフセットを指定します。まず. データセットの範囲 (存在する場合) は、パラメーターブロックの直後に続き、 **DataSetRangesOffset**は、範囲が開始される DEVICE_DSM_INPUT 構造体の先頭からのオフセットを指定します。 システムバッファー構造を次の図に示します。

![DSM IOCTL 入力バッファー](images/dsm_ioctl_inputbuffer.jpg)

管理アクションが出力を返す場合は、 [DEVICE_DSM_OUTPUT](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ns-ntddstor-_device_manage_data_set_attributes_output)構造体へのポインターが IOCTL の*outputbuffer*に渡されます。 アクションが追加のアクション固有の出力を返す場合、出力ブロックは DEVICE_DSM_OUTPUT 構造体の直後に続き、 **Outputblockoffset**は、DEVICE_DSM_OUTPUT 構造体の先頭からのオフセットを指定します。パラメーターブロックが開始されます。 出力バッファーの構造を次の図に示します。

![DSM IOCTL 出力バッファー](images/dsm_ioctl_outputbuffer.jpg)

DSM のプロセスフローについて以下に説明します。ここで、 *Sender*はアクション要求元と*ハンドラー*が要求されたアクションを処理します。 スタックには複数の*ハンドラー*が存在する場合があることに注意してください。

![DSM アクションフロー](images/dsm_action_flow.jpg)

1) *センダー*は DSM を初期化し、次の手順を実行して、スタック内の最初の*ハンドラー*に送信します。

   - アクションに関連付けられている定義を使用して、 [DEVICE_DSM_DEFINITION](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ns-ntddstor-_device_dsm_definition)構造体を割り当て、初期化します。
   - [**Devicedsmgetinputlength**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/nf-ntddstor-devicedsmgetinputlength)を呼び出して、アクションの入力バッファーに必要なサイズを決定し、このバッファーにメモリを割り当てます。
   - [**DeviceDsmInitializeInput**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/nf-ntddstor-devicedsminitializeinput)を呼び出して[DSM_DEVICE_INPUT](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ns-ntddstor-_device_manage_data_set_attributes)構造体を初期化し、アクションにパラメーターがある場合はパラメーター block を呼び出します。 パラメーターブロックの形式は、アクションによって異なります。 詳細については、 [DEVICE_DSM_ACTION の説明](device-dsm-action-descriptions.md)を参照してください。
   - アクションに範囲がある場合は、各範囲に対して[**Devicedsmadddatasetrange**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/nf-ntddstor-devicedsmadddatasetrange)を呼び出して、 [DEVICE_DSM_RANGE](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ns-ntddstor-_device_data_set_range)構造体を入力バッファーに追加します。
   - DSM に出力がある場合は、 [**Devicedsmgetoutputlength**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/nf-ntddstor-devicedsmgetoutputlength)を呼び出して、アクションの出力バッファーに必要なサイズを決定し、このバッファーにメモリを割り当てます。
   - [IOCTL_STORAGE_MANAGE_DATA_SET_ATTRIBUTES](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_manage_data_set_attributes)要求を送信し、初期化された入力データを IOCTL のシステムバッファーに渡します。割り当てられた出力バッファーがある場合は、それも渡します。

2) *ハンドラ*は、次の3つの方法のいずれかで DSM IOCTL 要求を処理します。
   1) 要求を処理し、出力がある場合はそれを返します。
   2) 要求を処理し、スタック内の次に小さいドライバーに転送します。
   3) DSM を処理せずに、スタック内の次に小さいドライバーに要求を転送します。

   > [!NOTE]
   > ドライバーが DSM を処理するかどうかにかかわらず、DEVICE_DSM_ACTION's の最上位ビット (**DeviceDsmActionFlag_NonDestructive**) が設定されて*いる場合にのみ*、要求を安全に転送できます。 **DeviceDsmActionFlag_NonDestructive**が設定されて*いない*場合、ドライバーはエラーを返します。
  
   *ハンドラー*が DSM を処理する場合、次の手順を実行します。

   - [**Devicedsmvalidateinput**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/nf-ntddstor-devicedsmvalidateinput)を呼び出して入力を検証します。
   - 入力が有効な場合、*ハンドラー*は入力を抽出してアクションを取得します。 アクションにパラメーターブロックがある場合、*ハンドラー*は[**Devicedsmparameterblock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/nf-ntddstor-devicedsmparameterblock)を呼び出してパラメーターブロックを取得します。 アクションに範囲データが含まれている場合、*ハンドラー*は[**DeviceDsmDataSetRanges**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/nf-ntddstor-devicedsmdatasetranges)を呼び出してデータセットの範囲のブロックへのポインターを取得し、ブロックに対して通常の処理を実行します。 このブロックは**DataSetRangesOffset**にあり、 [DEVICE_DSM_RANGE](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ns-ntddstor-_device_data_set_range)構造体として書式設定された1つ以上の連続するエントリで構成されます。 データセットの範囲の長さ (バイト単位) は、 [DEVICE_DSM_INPUT](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ns-ntddstor-_device_manage_data_set_attributes)の**DataSetRangesLength**メンバーで設定されます。
   - アクションに出力が必要な場合、*ハンドラー*は[**Devicedsmvalidateoutputlength**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/nf-ntddstor-devicedsmvalidateoutputlength)を呼び出して、送信元が指定した出力バッファーを検証します。 有効な場合、ハンドラーは[**DeviceDsmInitializeOutput**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/nf-ntddstor-devicedsminitializeoutput)を呼び出して出力バッファーの[DEVICE_DSM_OUTPUT](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ns-ntddstor-_device_manage_data_set_attributes_output)部分を初期化し、出力ブロックにアクション固有の出力がある場合はそれを設定します。 次に、*ハンドラー*は ioctl を完了し、ioctl をスタック内の次のドライバーに返すか、または転送します。

3) DSM が処理されて*送信者*に返されると、*送信*側は[**devicedsmvalidateoutput**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/nf-ntddstor-devicedsmvalidateoutput)を呼び出して出力を検証します (存在する場合)。 出力が有効な場合、*送信側*は[**Devicedsmoutputblock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/nf-ntddstor-devicedsmoutputblock)を呼び出すことによって出力ブロックを抽出します (存在する場合)。

特定の DSM アクションの詳細については、「[デバイス DSM アクションの説明](device-dsm-action-descriptions.md)」を参照してください。
