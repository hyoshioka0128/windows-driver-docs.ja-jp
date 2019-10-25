---
title: レポート検証
description: レポート検証
ms.assetid: 3731C877-1A69-447C-A5DB-0BDD1B753D3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b5fac8f52b7bf6a74506b22334e5e5e3a2587088
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840273"
---
# <a name="storport-verification"></a>レポート検証


## <span id="ddk_storport_verification_tools"></span><span id="DDK_STORPORT_VERIFICATION_TOOLS"></span>


Storport 検証機能は、Storport ミニポートドライバーとポートドライバーの間の相互作用を監視します。 ミニポートドライバーでルーチンが誤って使用されている場合、がポートドライバーからの要求に対して誤って応答するか、要求への応答に長時間かかる場合、バグチェックが発行されます。

**  Storport**検証機能は、windows Vista 以降のバージョンの windows でのみ使用できます。

 

### <a name="span-idviolations_detected_by_storport_verificationspanspan-idviolations_detected_by_storport_verificationspanviolations-detected-by-storport-verification"></a><span id="violations_detected_by_storport_verification"></span><span id="VIOLATIONS_DETECTED_BY_STORPORT_VERIFICATION"></span>Storport 検証によって検出された違反

Storport 検証機能では、誤って使用されている Storport ルーチンを検出できます。 また、これらのチェックの一部を個別に無効にすることもできます。

Storport の検証機能は、Storport ミニポートドライバーが次のいずれかの違反をコミットすると、バグチェック0xF1 またはバグチェック0xC4 を発行します。

-   ミニポートドライバーが、 [**Storportinitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportinitialize)ルーチンに無効な引数 (NULL ポインター) を渡しています。

-   ミニポートドライバーは[**Storportstallexecution**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportstallexecution)を呼び出し、0.1 秒より長い遅延時間を指定します。これにより、プロセッサが長時間停止します。

-   [**Storportfreedevicebase**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportfreedevicebase)は、ミニポートドライバーの**HwStorFindAdapter**ルーチンからのみ呼び出すことができます。

-   [**StorportgetHwStorFindAdapter Achedexテンション**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportgetuncachedextension)は、ミニポートドライバーのルーチンからのみ呼び出すことができ、バスマスターアダプターに対してのみ呼び出すことができます。 **Storportgetinitialization Achedexテンション**を呼び出す前に、ミニポートで、 [**HW\_初期化\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/ns-storport-_hw_initialization_data)(Storport) 構造の**srbextensionsize**を設定する必要があります。

-   [**Storportgetdevicebase**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportgetdevicebase)ルーチンは、システムプラグアンドプレイ (PnP) マネージャーによってドライバーに割り当てられたアドレスのみをサポートしています。

-   ミニポートドライバーは、**Storportread * * * xxx*または **StorPortWrite * * * Xxx*ルーチン ( [**Storportreadregisteruchar**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportreadregisteruchar)や[**StorPortWritePortBufferUlong**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportwriteportbufferulong)など) のいずれかに無効な仮想アドレスを渡します。 これは通常、指定されたアドレスが共通のバッファー領域にマップされないことを意味します。 指定された*レジスタ*または*ポート*は、 [**storportgetdevicebase**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportgetdevicebase)ルーチンによって返されるマップされたメモリ領域の範囲内である必要があります。 このチェックは、x86 ベースのシステムでのみサポートされています。

Storport 検証で使用されるバグチェックパラメーターの一覧については、「 [**Bug Check 0xF1**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xf1--scsi-verifier-detected-violation) (SCSI\_VERIFIER\_検出された\_違反)」を参照してください。 Storport 検証では、バグチェック0xF1 に加えて、[**バグチェック 0xC4**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation) (DRIVER\_VERIFIER\_検出された\_違反) も使用します。

**注**  [**バグチェック 0XF1**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xf1--scsi-verifier-detected-violation)は、SCSI 検証と Storport 検証の両方に使用されます。

 

### <a name="span-idactivating_this_optionspanspan-idactivating_this_optionspanactivating-this-option"></a><span id="activating_this_option"></span><span id="ACTIVATING_THIS_OPTION"></span>このオプションをアクティブにする

Storport 検証オプションをアクティブにする手順は、他のドライバー検証ツールオプションをアクティブにする手順とは異なります。

**Storport 検証をアクティブ化するには**

1.  Driver Verifier マネージャーまたは*Verifier*コマンドラインを使用して、ミニポートドライバーの検証を開始します。 Storport 検証はオプションとして使用できないため、*他の*ドライバー検証ツールオプションを少なくとも1つ選択する必要があります。 詳細については、「[ドライバーの検証オプションの選択](selecting-driver-verifier-options.md)」および「[検証するドライバーの選択](selecting-drivers-to-be-verified.md)」を参照してください。

2.  *Regedit.exe*を使用してレジストリを開きます。 **HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\StorPort**キーで、 **Verifier**という名前のサブキーを追加します。 **StorPort**キーが存在しない場合は、作成する必要があります。 **HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\STORPort\\Verifier**キーで、 **verifylevel**という名前の**REG\_DWORD**エントリを追加します。 このエントリに割り当てられた値によって、どの Storport 検証テストがアクティブになるかが決まります。 値0x1 は、最大の検証を行います。

3.  コンピューターを再起動します。

**Verifylevel**値が存在しない場合、または0xffffffff と等しい場合、Storport 検証は無効になります。

### <a name="span-idactivating_without_rebootingspanspan-idactivating_without_rebootingspanactivating-without-rebooting"></a><span id="activating_without_rebooting"></span><span id="ACTIVATING_WITHOUT_REBOOTING"></span>再起動せずにアクティブ化する

一般に、Windows オペレーティングシステムでコンピューターを再起動 (再起動) せずに、Storport 検証をアクティブ化または非アクティブ化することはできません。 *StorPort*ドライバーは、が読み込まれるときにのみ**verifylevel**レジストリエントリを読み取ります。これは通常、ブート時に実行されます。 ただし、レジストリエントリを追加したときに*storport*ドライバーが読み込まれていない場合、またはアンロードされて再度読み込まれた場合は、コンピューターを再起動しなくても、windows Vista 以降のバージョンの Windows で storport 検証を有効にすることができます。

 

 





