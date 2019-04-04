---
title: WHEA によって実行される PFA
description: WHEA によって実行される PFA
ms.assetid: c93b15aa-9b99-4dfa-8c97-b503654e44f2
keywords:
- 予測的な失敗の分析 (PFA) WDK WHEA、エラー訂正コードのメモリ
- PFA WDK WHEA、エラー訂正コードのメモリ
- エラー訂正コード メモリ WDK WHEA
- エラー訂正コード メモリ WDK WHEA、予測的な失敗の分析
- 低レベル ハードウェア エラー ハンドラー WDK WHEA
- LLHEH WDK WHEA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 93c872d0fa9c58e75df5c763fc8a12075383b8e3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528189"
---
# <a name="pfa-performed-by-whea"></a>WHEA によって実行される PFA


Windows 7 以降、Windows ハードウェア エラー アーキテクチャ (WHEA) は、エラー修正コード (ECC) メモリの予測的な障害の分析 (PFA) をサポートします。

**重要な**  A[プラットフォーム固有のハードウェア エラー ドライバー (PSHED) プラグイン](platform-specific-hardware-error-driver-plug-ins2.md)WHEA ではなく ECC メモリ PFA を実行することができます。 プラグイン PFA を実行する場合で説明されている手順に従う必要があります[PFA 実行プラグイン PSHED](pfa-performed-by-a-pshed-plug-in.md)します。 プラグインする必要があります」の手順は、このトピックで後述します。

 

ECC メモリ エラーが発生したときに、WHEA は、次の手順を実行します。

1.  *低レベル ハードウェア エラー ハンドラー* (*LLHEH*) メモリ エラーの状態の有無について通知されます。

2.  LLHEH では、エラーのソースからメモリ エラーの情報を取得し、エラー データを使用して、ハードウェアのエラー パケットを入力します。 このパケットとして書式設定、 [WHEA\_エラー\_パケット](https://msdn.microsoft.com/library/windows/hardware/ff560465)構造体。

3.  任意のプラットフォーム固有のハードウェア エラー情報を取得、PSHED に LLHEH 呼び出し。 PSHED のプラグインでは、インストールし、エラーに関する情報を取得するが登録されている、PSHED を呼び出す、PSHED プラグイン プラグインは、LLHEH に返されるエラー情報を変更できるようにします。

4.  LLHEH エラー パケットを渡して、Windows オペレーティング システム カーネルを呼び出します。

5.  Windows カーネルの作成、[エラー レコード](error-records.md)し、LLHEH から受信したエラー パケットの情報を追加します。 さらに、Windows カーネルを追加、エラーに関する他の情報 (エラーの発生元、およびそのエラーの回数をエラーの重大度が発生しました) とエラー レコードにします。

6.  Windows カーネルへの呼び出し、PSHED にエラー レコードにセクションを追加するよう PSHED を許可します。

7.  PSHED のプラグインがインストールされ、エラーに関する情報を取得するが登録されている場合、PSHED を呼び出す、PSHED プラグイン プラグインはエラー レコードの情報を変更できるようにします。

    **注**  これを設定する必要がありますしないプラグインの PSHED に PFA が実行していない場合、 **PlatformPfaControl**ビット、 [ **WHEA\_エラー\_パケット\_フラグ**](https://msdn.microsoft.com/library/windows/hardware/ff560472)のメンバー、 [WHEA\_エラー\_パケット](https://msdn.microsoft.com/library/windows/hardware/ff560465)構造体。

     

8.  PFA が有効になっている場合、WHEA は ECC メモリ ページで PFA を実行します。 このプロセスの詳細については、[方法 WHEA 実行 PFA ECC メモリ](how-whea-performs-pfa-on-ecc-memory.md)を参照してください。

9.  Windows カーネルでは、ETW イベントを生成し、システム イベント ログにエラー情報を記録します。

 

 




