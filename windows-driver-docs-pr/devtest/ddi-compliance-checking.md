---
title: DDI 準拠の検査
description: DDI の準拠チェックオプションは、ドライバーが Windows オペレーティングシステムのカーネルと正しく通信するかどうかを決定します。
ms.assetid: 1E536DE0-071B-4529-B228-DB5DAE71099C
ms.date: 04/03/2020
ms.localizationpriority: medium
ms.openlocfilehash: d42be38216c925e45614a01cf6a8a15bcead9a27
ms.sourcegitcommit: 84be9e06fd0886598df77dffcbc75632d613c8f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/11/2020
ms.locfileid: "81217170"
---
# <a name="ddi-compliance-checking"></a>DDI 準拠の検査

DDI の準拠チェックオプションは、ドライバーが Windows オペレーティングシステムのカーネルと正しく通信するかどうかを決定します。

**メモ** このオプションは、Windows 8 以降で使用できます。 Windows 8.1 から、[ [DDI 準拠の確認 (追加)] オプション](#activating-the-ddi-compliance-checking-additional-option)を選択して追加のルールをテストできます。

| DDI 準拠の検査 |
|-------------------------|
|                         |

[DDI 準拠の確認] オプションでは、[静的ドライバーの検証ツール](static-driver-verifier.md)が使用するのと同じデバイスドライバーインターフェイス (DDI) の使用規則が適用されます。この規則は、ドライバーが関数の呼び出しを必要としているかどうかを検証するために、またはスピンロックを適切に取得して解放します。

このオプションが有効になっていて、ドライバーの検証ツールで、いずれかの DDI コンプライアンス規則に違反していることが検出された場合、ドライバーの検証ツールはバグチェック 0xC4 (パラメーター1は特定のコンプライアンス規則の識別子と同じ) を発行します。

[DDI 準拠チェック] オプションを選択すると、次の規則が含まれます。

[**GuardedRegions**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-guardedregions) (Windows 8.1 から開始)

[**IoSetCompletionExCompleteIrp**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-iosetcompletionexcompleteirp) (Windows 8.1 から開始)

[**IrqlApcLte**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlapclte)

[**IrqlDispatch**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqldispatch)

[**IrqlExAllocatePool**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlexallocatepool)

[**IrqlExApcLte1**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlexapclte1)

[**IrqlExApcLte2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)

[**IrqlExApcLte3**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlexapclte3)

[**IrqlExPassive**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlexpassive)

[**IrqlIoApcLte**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlioapclte)

[**IrqlIoDispatch**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqliodispatch)

[**IrqlIoPassive1**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqliopassive1)

[**IrqlIoPassive2**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqliopassive2)

[**IrqlIoPassive3**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqliopassive3)

[**IrqlIoPassive4**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqliopassive4)

[**IrqlIoPassive5**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqliopassive5)

[**IrqlKeApcLte1**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlkeapclte1)

[**IrqlKeApcLte2**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlkeapclte2)

[**IrqlKeDispatchLte**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlkedispatchlte)

[**IrqlKeReleaseSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlkereleasespinlock)

[**IrqlKeSetEvent**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlkesetevent)

[**IrqlMmApcLte**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlmmapclte)

[**IrqlMmDispatch**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlmmdispatch)

[**IrqlObPassive**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlobpassive)

[**IrqlPsPassive**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlpspassive)

[**Irqlreturn**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlreturn) (Windows 8.1 から開始)

[**IrqlRtlPassive**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlrtlpassive)

[**IrqlZwPassive**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlzwpassive)

[**NdisOidComplete**](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-ndisoidcomplete) (Windows 8.1 から開始)

[**NdisOidDoubleComplete**](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-ndisoiddoublecomplete) (Windows 8.1 から開始)

[**PnpRemove**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-pnpremove) (Windows 8.1 から開始)

[**Requestedpowerirp**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-requestedpowerirp) (Windows 8.1 以降)

[**QueuedSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-queuedspinlock) (Windows 8.1 から開始)

[**スピンロック**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-spinlock)(Windows 8.1 から開始)

現在、これら2つの規則は省略可能ですが、推奨されます。

[Optional**Irqlntifsapcpassive**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlntifsapcpassive)

[Optional**IrqlIoRtlZwPassive**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqliortlzwpassive)

## <a name="span-idactivating_the_ddi_compliance_checking_optionspanspan-idactivating_the_ddi_compliance_checking_optionspanspan-idactivating_the_ddi_compliance_checking_optionspanactivating-the-ddi-compliance-checking-option"></a><span id="Activating_the_DDI_compliance_checking_option"></span><span id="activating_the_ddi_compliance_checking_option"></span><span id="ACTIVATING_THE_DDI_COMPLIANCE_CHECKING_OPTION"></span>DDI 準拠チェックオプションのアクティブ化

1つまたは複数のドライバーに対して、Driver Verifier マネージャーまたは Verifier コマンドラインを使用して、DDI のコンプライアンスチェック機能をアクティブ化することができます。 詳細については、「[ドライバーの検証オプションの選択](selecting-driver-verifier-options.md)」を参照してください。 DDI 準拠チェックオプションをアクティブ化または非アクティブ化するには、コンピューターを再起動する必要があります。 標準設定 ( **/標準**) を使用すると、DDI の準拠確認機能がアクティブ化されます。

-   **コマンドラインで**

    コマンドラインでは、DDI 準拠の確認は、 **verifier/flags 0x00020000** (ビット 17) によって表されます。 DDI 準拠チェックをアクティブにするには、フラグ値0x00020000 を使用するか、フラグ値に0x00020000 を追加します。 例 :

    ```
    verifier /flags 0x00020000 /driver MyDriver.sys
    ```

    この機能は、次回の起動時にアクティブになります。

-   **ドライバー検証マネージャーの使用**

    1.  ドライバー検証マネージャーを起動します。 コマンドプロンプトウィンドウで「 **Verifier** 」と入力します。
    2.  [**カスタム設定の作成] (コード開発者向け)** を選択し、 **[次へ]** をクリックします。
    3.  [**完全な一覧から個々の設定を選択]** を選択します。
    4.  **[DDI 準拠の確認]** チェックボックスをオンにします。
    5.  コンピューターを再起動します。

## <span id="DDI_compliance_checking_additional"></span><span id="ddi_compliance_checking_additional"></span><span id="DDI_COMPLIANCE_CHECKING_ADDITIONAL"></span>


| DDI 準拠の確認 (追加) |
|--------------------------------------|
|                                      |

Windows 8.1 以降では、[ **DDI 準拠チェック] (追加) オプション**を選択すると、ドライバーが Windows オペレーティングシステムのカーネルと正しく対話するかどうかを判断するための追加の規則が提供されます。 [ **DDI 準拠の確認 (追加)] オプション**を選択すると、次の規則がテストされます。

- [**CriticalRegions**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-criticalregions)

- [**QueuedSpinLockRelease**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-queuedspinlockrelease)

- [**SpinlockRelease**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-spinlockrelease)

## <a name="activating-the-ddi-compliance-checking-additional-option"></a>DDI 準拠チェックのアクティブ化 (追加) オプション

1つまたは複数のドライバーに対して、ドライバー検証マネージャーまたは Verifier コマンドラインを使用して、 **DDI 準拠チェック (追加)** 規則をアクティブにすることができます。 詳細については、「[ドライバーの検証オプションの選択](selecting-driver-verifier-options.md)」を参照してください。 **DDI 準拠の確認 (追加)** オプションをアクティブ化または非アクティブ化するには、コンピューターを再起動する必要があります。

-   **コマンドラインで**

    コマンドラインでは、DDI のコンプライアンスチェックは、 **verifier/flags 0x00080000** (ビット 19) によって表されます。 DDI 準拠チェックをアクティブにするには **(追加)** 、フラグ値として0x00080000 を使用するか、フラグ値に0x00080000 を追加します。 例 :

    ```
    verifier /flags 0x00080000 /driver MyDriver.sys
    ```

    この機能は、次回の起動時にアクティブになります。

-   **ドライバー検証マネージャーの使用**

    1.  ドライバー検証マネージャーを起動するには、コマンドプロンプトウィンドウで「 **verifier** 」と入力します。
    2.  [**カスタム設定の作成] (コード開発者向け)** を選択し、 **[次へ]** をクリックします。
    3.  [**完全な一覧から個々の設定を選択]** を選択します。
    4.  **[DDI 準拠の確認 (追加)]** を選択します。
    5.  コンピューターを再起動します。

## <a name="activating-the-ddi-compliance-checking-additional-irql-option"></a>DDI 準拠の確認 (追加の IRQL) オプションのアクティブ化

1つまたは複数のドライバーについて、nuget.exe コマンドラインを使用して、DDI 準拠の追加の IRQL 規則をアクティブにすることができます。 詳細については、「[ドライバーの検証オプションの選択](selecting-driver-verifier-options.md)」を参照してください。 DDI 準拠の追加の IRQL 規則をアクティブ化または非アクティブ化するには、コンピューターを再起動する必要があります。

コマンドラインでは、DDI 準拠の追加の IRQL チェックは、規則クラス値35で表されます。 例 :

`verifier /ruleclasses 35 /driver MyDriver.sys`

または

`verifier /rc 35 /driver MyDriver.sys`

追加の IRQL 規則セットは、次の2つの規則で構成されます。

[Optional**Irqlntifsapcpassive**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlntifsapcpassive)

[Optional**IrqlIoRtlZwPassive**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqliortlzwpassive)


