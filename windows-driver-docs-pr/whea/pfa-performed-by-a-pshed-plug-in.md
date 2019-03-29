---
title: PSHED プラグインによって実行される PFA
description: PSHED プラグインによって実行される PFA
ms.assetid: e9876c86-b059-406f-a01a-7670ab294098
keywords:
- 予測的な失敗の分析 (PFA) WDK WHEA、PSHED プラグイン
- PFA WDK WHEA、PSHED プラグイン
- プラットフォーム固有のハードウェア エラー ドライバー (PSHED) WDK WHEA
- プラットフォーム固有のハードウェア エラー ドライバー (PSHED) WDK WHEA、予測的な失敗の分析
- PSHED プラグイン WDK WHEA
- PSHED プラグイン WDK WHEA、予測的な失敗の分析
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5af8d68b752f26498610979d2eae8237a216ef7d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574929"
---
# <a name="pfa-performed-by-a-pshed-plug-in"></a>PSHED プラグインによって実行される PFA


A[プラットフォーム固有のハードウェア エラー ドライバー (PSHED) プラグイン](platform-specific-hardware-error-driver-plug-ins2.md)ECC メモリで予測的な障害の分析 (PFA) を実行することができます。 この場合、プラグインと WHEA ではありませんが ECC メモリ ページを監視する必要があります。 プラグインは、ECC メモリ ページが、エラーのしきい値を超えたことを判断した場合は、WHEA には、このステータスを示します。 WHEA は、[メモリ] ページをオフラインにしようとします。

**注**PSHED プラグインが PFA を実行し、レジストリを使用して、エラーのしきい値やタイムアウト、監視などその構成設定を保存する場合、したりしないでください依存で説明されている WHEA PFA 構成設定を使用して[WHEAポリシーの設定](whea-pfa-registry-settings.md)します。



ECC メモリ エラーが発生したときに WHEA およびプラグインは、次の手順に従います。

1.  *低レベル ハードウェア エラー ハンドラー* (*LLHEH*) メモリ エラーの状態の有無について通知されます。

2.  LLHEH では、エラーのソースからメモリ エラーに関する情報を取得し、エラー データを使用して、ハードウェアのエラー パケットを完了します。 このパケットとして書式設定、 [WHEA\_エラー\_パケット](https://msdn.microsoft.com/library/windows/hardware/ff560465)構造体。

3.  任意のプラットフォーム固有のハードウェア エラー情報を取得、PSHED に LLHEH 呼び出し。 PSHED でプラグインがインストールされ、エラーに関する情報を取得するが登録されている場合、PSHED は呼び出します、PSHED にプラグインできるように、プラグインは、LLHEH に返されるエラーに関する情報を変更できます。

4.  LLHEH では、Windows オペレーティング システムのカーネルの呼び出しをエラー パケットを渡します。

5.  Windows カーネルの作成、[エラー レコード](error-records.md)し、LLHEH から受信したエラー パケットの情報を追加します。 さらに、エラー レコードにエラーが発生したエラーの発生元、何回か、エラーの重大度などの Windows カーネルには、エラーに関する他の情報が追加されます。

6.  Windows カーネルへの呼び出し、PSHED にエラー レコードにセクションを追加するよう PSHED を許可します。

7.  PSHED のプラグインがインストールされ、エラー情報を取得するが登録されている場合、PSHED を呼び出す、PSHED プラグイン エラー レコードの情報を変更できるようにします。

8.  プラグインの PSHED が ECC メモリ ページで PFA に実行している場合は、以下を行うこと必要があります。

    -   設定、 **PlatformPfaControl**ビット、 [ **WHEA\_エラー\_パケット\_フラグ**](https://msdn.microsoft.com/library/windows/hardware/ff560472)のメンバー、 [WHEA\_エラー\_パケット](https://msdn.microsoft.com/library/windows/hardware/ff560465)構造体。 このビットが設定されている場合、WHEA は不要になったに PFA メモリ ページに責任を負います。
    -   プラグイン、認識された場合、エラーが発生した ECC メモリ ページが取得されることオフライン設定、 **PlatformDirectedOffline**ビット、 [ **WHEA\_エラー\_パケット\_フラグ**](https://msdn.microsoft.com/library/windows/hardware/ff560472)メンバー。 このビットが設定されている場合、WHEA はメモリのページをオフラインにしようとします。

    それ以外の場合、プラグインの PSHED をオフにする必要があります、 **PlatformPfaControl**と**PlatformDirectedOffline**ビットで、 [ **WHEA\_エラー\_パケット\_フラグ**](https://msdn.microsoft.com/library/windows/hardware/ff560472)のメンバー、 [WHEA\_エラー\_パケット](https://msdn.microsoft.com/library/windows/hardware/ff560465)構造体。

    **注**場合、 **PlatformPfaControl**ビットがクリアされて、そのように構成、およびオフライン ECC メモリ ページのエラーが発生する必要があるかどうかを決定する場合、WHEA が PFA を実行します。 このプロセスの詳細については、次を参照してください。 [PFA が WHEA によって実行される](pfa-performed-by-whea.md)します。



9.  場合は、ECC メモリ ページはオフラインにする必要があります、WHEA まず呼び出し、システム メモリ マネージャーはこの操作を実行します。

    **注**システムのメモリ マネージャーが呼び出されたときに、ECC メモリ ページが実際にオフラインされる保証はありません。




次に、WHEA は、システムのブート構成データ (BCD) ストアに、メモリ ページを追加します。 これは、メモリ ページが次のシステム再起動後に使用されていることを防ぎます。

**注**WHEA になります、ECC メモリ ページなどのハードウェア コンポーネント オフライン場合、レジストリ値**DisableOffline** 0 以外の値に設定されています。 また、WHEA はページを追加できません、メモリ、BCD ストアを場合、レジストリ値**MemPersistOffline** 0 に設定されます。 レジストリ値の詳細については、次を参照してください。 [WHEA ポリシー設定](whea-pfa-registry-settings.md)します。



システムのメモリ マネージャーの詳細については、次を参照してください。[メモリ管理](https://go.microsoft.com/fwlink/p/?linkid=140723)Windows SDK のドキュメント。


10. Windows カーネルでは、ETW イベントを生成し、システム イベント ログにエラー情報を記録します。








