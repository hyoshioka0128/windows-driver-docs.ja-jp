---
title: デュアル SIM
description: デュアル SIM
ms.assetid: 18521fec-c9fb-48d0-9de2-d0482e4807d6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ba7b3aa144a62d7465ecffcaa45f61d209f5d703
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372714"
---
# <a name="dual-sim"></a>デュアル SIM


Windows Phone 8.1 以降では、デュアル SIM デュアル アクティブ (DSDA) とデュアル デュアル SIM スタンバイ (DSDS) をサポートします。 DSDA、音声通話と SMS 両方の行に同時にできます。 DSDS により、両方の行で、登録して、呼び出しは、いずれかの行から受信した/作成できます。 ただし、1 つだけの行は、特定の時点の音声通話にできます。 DSDA と DSDS の両方のデータは、1 行のみに制限されます。

W/G + G. Windows Phone 8.1 以降をサポートしています

Windows Phone 8.1 GDR1 には、C + G. サポートが追加されます。

## <a name="architecture"></a>Architecture


各 UICC スロットは、エグゼキュータに関連付けられます。 Executor は、特定の移動体通信ネットワークに登録し、ハンドルの携帯電話に関連するタスクなどを行うと、通話と SMS を受信します。

### <a name="wg--g"></a>W/G + G

持つラジオ型 W/G + G 携帯電話の 1 つの executor が W/G 対応にあり、1 つの executor が G 対応します。 ユーザーがデータ行に使用するが、UICC スロットによっては、そのスロットは自動的により高機能な W/G エグゼキュータに関連付けられています。 次の図は、UICC のスロットに、ユーザーがデータ行の選択に応じて 2 つの可能な実行プログラムの関連付けを表示します。

![hwcomponents\-dualsim\-論理ビュー\-1](images/hwcomponents-dualsim-logicalview.png)![hwcomponents\-dualsim\-論理ビュー\-2](images/hwcomponents-dualsim-logicalview-2.png)

### <a name="cg"></a>C + G

C + G を入力するオプションがあるデバイスの場合は、CDMA UICC が常に含まれるスロットは、executor 0 を使用します。 2 つの GSM UICCs がある場合は、データ行の選択 UICC は executor 0 に関連付けられます。

C + G を構成する方法の詳細については、次を参照してください。[デュアル SIM 設定の構成 C + G](https://msdn.microsoft.com/library/windows/hardware/dn757414)します。

## <a name="uicc-swapping"></a>UICC スワップ


いずれかのスロット UICC のホット削除がサポートされています。 UICC の削除時に関連付けられている executor はサービスが失われます、ダイアログ ボックスが表示されます。 UICCs のホットな挿入がサポートされていません。 起動後に新しい UICC が挿入される場合、デバイスが登録されていないは残ります。

手動の APNs 設定などの特定のユーザー設定の UICC は UICC ごとに保存され、UICC が再度挿入されるときに復元されます。

## <a name="airplane-mode"></a>機内モード


機内モードをオンにすることは、両方の行の携帯電話をオフにします。 ユーザーを携帯電話の行をオンに機内モードでは、機内モードをオフにするのには、プロンプトが表示されます。

## <a name="pin-lock"></a>PIN ロック


PIN1、暗証番号 2、および PUK が両方 UICCs のサポートされています。

## <a name="sim-toolkit"></a>SIM ツールキット


UTK は、両方の UICCs でサポートされます。 UTK UI は、一度に 1 つだけ UICC でサポートされます。

両方の UICC スロットのリセット UTK コマンドを使用して UICC 更新はサポートされています。

 

 





