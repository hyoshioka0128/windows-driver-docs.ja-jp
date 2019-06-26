---
title: DDI 準拠の検査
description: DDI 準拠チェックのオプションは、Windows オペレーティング システムのカーネルのドライバーが正しく対話するかどうかを決定します。
ms.assetid: 1E536DE0-071B-4529-B228-DB5DAE71099C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6ff62733a6c15f04199e7d14cd07395a8b870338
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371573"
---
# <a name="ddi-compliance-checking"></a>DDI 準拠の検査


DDI 準拠チェックのオプションは、Windows オペレーティング システムのカーネルのドライバーが正しく対話するかどうかを決定します。

**注**このオプションは Windows 8 以降で使用できます。 Windows 8.1 以降、テストできます追加の規則を選択して[DDI 準拠の検査 (追加) オプションをアクティブ化する](#activating-the-ddi-compliance-checking-additional-option)します。



| DDI 準拠の検査 |
|-------------------------|
|                         |

DDI 準拠の検査オプションが適用される同じデバイス ドライバー インターフェイス (DDI) の使い方の規則を[Static Driver Verifier](static-driver-verifier.md)を使用して、ドライバーが、関数の適切な IRQL で関数呼び出しを行うことを確認または正常取得し、スピンロックを解放します。

Driver Verifier では、このオプションがアクティブで、Driver Verifier は、ドライバーが違反 DDI 準拠の規則のいずれかを検出 (パラメーター 1 が特定のコンプライアンス規則の識別子に等しい) でのバグ チェック 0xC4 が発行されます。

DDI 準拠の検査オプションを選択すると、次の規則が含まれます。

[**GuardedRegions** ](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-guardedregions) (Windows 8.1 以降)

[**IoSetCompletionExCompleteIrp** ](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-iosetcompletionexcompleteirp) (Windows 8.1 以降)

[**IrqlApcLte**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlapclte)

[**IrqlDispatch**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqldispatch)

[**IrqlExAllocatePool**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlexallocatepool)

[**IrqlExApcLte1**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlexapclte1)

[**IrqlExApcLte2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)

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

[**IrqlReturn** ](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlreturn) (Windows 8.1 以降)

[**IrqlRtlPassive**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlrtlpassive)

[**IrqlZwPassive**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlzwpassive)

[**NdisOidComplete** ](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-ndisoidcomplete) (Windows 8.1 以降)

[**NdisOidDoubleComplete** ](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-ndisoiddoublecomplete) (Windows 8.1 以降)

[**PnpRemove** ](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-pnpremove) (Windows 8.1 以降)

[**RequestedPowerIrp** ](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-requestedpowerirp) (Windows 8.1 以降)

[**QueuedSpinLock** ](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-queuedspinlock) (Windows 8.1 以降)

[**SpinLock** ](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-spinlock) (Windows 8.1 以降)

## <a name="span-idactivatingtheddicompliancecheckingoptionspanspan-idactivatingtheddicompliancecheckingoptionspanspan-idactivatingtheddicompliancecheckingoptionspanactivating-the-ddi-compliance-checking-option"></a><span id="Activating_the_DDI_compliance_checking_option"></span><span id="activating_the_ddi_compliance_checking_option"></span><span id="ACTIVATING_THE_DDI_COMPLIANCE_CHECKING_OPTION"></span>DDI 準拠の検査オプションがアクティブ化します。


機能の 1 つまたは複数のドライバーをドライバー検証マネージャーまたは Verifier.exe コマンドラインを使用してチェック DDI 準拠を有効にすることができます。 詳細については、次を参照してください。[ドライバー検証ツールのオプションの選択](selecting-driver-verifier-options.md)します。 DDI 準拠の検査オプションがアクティブまたは非アクティブにコンピューターを再起動する必要があります。 DDI 準拠チェック機能をアクティブにすると、標準の設定を使用する場合 (**標準/** )。

-   **コマンドラインで**

    、コマンドラインで DDI 準拠の検査で表される**verifier/flags 0x00020000** (ビット 17)。 DDI 準拠のチェックを有効にするには、0x00020000 のフラグの値を使用して、または 0x00020000 をフラグ値に追加します。 次に、例を示します。

    ```
    verifier /flags 0x00020000 /driver MyDriver.sys
    ```

    この機能は、[次へ] の起動後にアクティブになります。

-   **ドライバー検証マネージャーを使用します。**

    1.  ドライバー検証マネージャーを起動します。 型**Verifier**コマンド プロンプト ウィンドウでします。
    2.  選択 **(コード開発者) 用のカスタム設定を作成する**順にクリックします**次**します。
    3.  選択**完全な一覧から個々 の設定を選択します。** します。
    4.  選択 (チェック) **DDI 準拠の検査**します。
    5.  コンピューターを再起動します。

## <span id="DDI_compliance_checking_additional"></span><span id="ddi_compliance_checking_additional"></span><span id="DDI_COMPLIANCE_CHECKING_ADDITIONAL"></span>


| DDI 準拠のチェック (追加) |
|--------------------------------------|
|                                      |

Windows 8.1 では、以降、 **DDI 準拠の検査 (追加) オプション**オプションには、Windows オペレーティング システムのカーネルのドライバーが正しく対話するかどうかを判断する追加の規則が用意されています。 選択すると、 **DDI 準拠の検査 (追加) オプション**、次のルールがテストされます。

-   [**CriticalRegions**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-criticalregions)

-   [**QueuedSpinLockRelease**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-queuedspinlockrelease)

-   [**SpinlockRelease**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-spinlockrelease)

## <a name="activating-the-ddi-compliance-checking-additional-option"></a>DDI 準拠の検査 (追加) オプションをアクティブ化します。


アクティブ化することができます、 **DDI 準拠の確認 (追加)** ドライバー検証マネージャーまたは Verifier.exe コマンドラインを使用して 1 つまたは複数のドライバの規則。 詳細については、次を参照してください。[ドライバー検証ツールのオプションの選択](selecting-driver-verifier-options.md)します。 アクティブ化または非アクティブ化するコンピューターを再起動する必要があります、 **DDI 準拠の確認 (追加)** オプション。

-   **コマンドラインで**

    、コマンドラインで DDI 準拠の検査で表される**verifier/flags 0x00080000** (ビット 19)。 アクティブ化する**DDI 準拠の確認 (追加)** 0x00080000 のフラグの値を使用して、または、0x00080000 をフラグ値に追加します。 次に、例を示します。

    ```
    verifier /flags 0x00080000 /driver MyDriver.sys
    ```

    この機能は、[次へ] の起動後にアクティブになります。

-   **ドライバー検証マネージャーを使用します。**

    1.  ドライバー検証マネージャーを起動します。 型**Verifier**コマンド プロンプト ウィンドウでします。
    2.  選択 **(コード開発者) 用のカスタム設定を作成する**順にクリックします**次**します。
    3.  選択**完全な一覧から個々 の設定を選択します。** します。
    4.  選択 (チェック) **DDI 準拠の確認 (追加)** します。
    5.  コンピューターを再起動します。









