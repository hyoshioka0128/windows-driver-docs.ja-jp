---
title: PSHED プラグインによって実行される PFA
description: PSHED プラグインによって実行される PFA
ms.assetid: e9876c86-b059-406f-a01a-7670ab294098
keywords:
- 予測エラー分析 (PFA) WDK WHEA、PFA プラグイン
- PFA WDK WHEA、PFA プラグイン
- プラットフォーム固有のハードウェアエラードライバー (PSHED) WDK WHEA
- プラットフォーム固有のハードウェアエラードライバー (PSHED) WDK WHEA、予測エラー分析
- PSHED プラグイン WDK WHEA
- PSHED プラグイン WDK WHEA、予測エラー分析
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 15fdfd571a43e0d4114fb8b490fb6302d836a2d1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837996"
---
# <a name="pfa-performed-by-a-pshed-plug-in"></a>PSHED プラグインによって実行される PFA


[プラットフォーム固有のハードウェアエラードライバー (pshed) プラグイン](platform-specific-hardware-error-driver-plug-ins2.md)は、ECC メモリで予測エラー分析 (pshed) を実行できます。 この問題が発生した場合、WHEA ではなくプラグインが ECC メモリページを監視する必要があります。 プラグインによって、ECC メモリページがエラーしきい値を超えたと判断された場合、この状態は WHEA になります。 次に、WHEA はメモリページをオフラインにしようとします。

**メモ** Pshed プラグインが PSHED を実行し、レジストリを使用して、エラーのしきい値やタイムアウトの監視などの構成設定を格納している場合は、「 [Whea ポリシー設定](whea-pfa-registry-settings.md)」に記載されている WHEA pshed 構成設定に依存したり、使用したりしないでください。



ECC メモリエラーが発生した場合、WHEA とプラグインは次の手順を実行します。

1.  *低レベルのハードウェアエラーハンドラー* (*LLHEH*) には、メモリエラー状態の有無が通知されます。

2.  LLHEH は、エラーソースからメモリエラーに関する情報を取得し、エラーデータを使用してハードウェアエラーパケットを完了します。 このパケットは、 [WHEA\_エラー\_パケット](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff560465(v=vs.85))構造として書式設定されます。

3.  LLHEH は、プラットフォーム固有のハードウェアエラー情報を取得するために、を呼び出します。 がインストールされていて、エラーに関する情報を取得するように登録されている場合は、LLHEH に返されるエラーに関する情報をプラグインが変更できるように、pshed プラグインが呼び出されます。

4.  LLHEH は、Windows オペレーティングシステムカーネルを呼び出し、それにエラーパケットを渡します。

5.  Windows カーネルは[エラーレコード](error-records.md)を作成し、LLHEH から受信したエラーパケットの情報を追加します。 さらに、Windows カーネルによって、エラーに関する他の情報 (エラーソース、エラーの重大度、エラーが発生した回数など) がエラーレコードに追加されます。

6.  Windows カーネルは、エラーレコードにセクションを追加できるようにするために、を呼び出します。

7.  問題のあるプラグインがインストールされていて、エラー情報を取得するために登録されている場合は、エラーレコードの情報を変更できるように、pshed プラグインが呼び出されます。

8.  PSHED プラグインが ECC メモリページで PSHED を実行している場合は、次の操作を行う必要があります。

    -   Whea [ **\_error\_packet\_FLAGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_whea_error_packet_flags)メンバーの**PlatformPfaControl**ビットを設定して、 [whea\_エラー\_パケット](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff560465(v=vs.85))構造にします。 このビットが設定されている場合、そのメモリページの PFA は WHEA ではなくなります。
    -   プラグインによって、エラーが発生した ECC メモリページをオフラインにする必要があると判断された場合は、 [**WHEA\_error\_PACKET\_FLAGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_whea_error_packet_flags)メンバーに**Platformdirectedoffline**ビットを設定します。 このビットが設定されている場合、WHEA はメモリページをオフラインにしようとします。

    それ以外の場合は、whea [ **\_エラー\_パケット\_フラグ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_whea_error_packet_flags)のメンバーである WHEA [\_エラー\_パケット](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff560465(v=vs.85))に含まれる、 **PlatformPfaControl**および**platformdirectedoffline 行**ビットをクリアする必要があります。データ.

    **メモ** **PlatformPfaControl**ビットがオフの場合、WHEA は構成されている場合は pfa を実行し、エラーが発生した ECC メモリページをオフラインにする必要があるかどうかを判断します。 このプロセスの詳細については、「 [WHEA によって実行される Pfa](pfa-performed-by-whea.md)」を参照してください。



9.  ECC メモリページをオフラインにする必要がある場合、WHEA はまずシステムメモリマネージャーを呼び出してこの操作を実行します。

    **メモ** システムメモリマネージャーを呼び出すと、ECC メモリページが実際にオフラインになるという保証はありません。




次に、WHEA は、メモリページをシステム上のブート構成データ (BCD) ストアに追加します。 これにより、次回のシステム再起動後にメモリページが使用されなくなります。

**メモ** レジストリ値**Disableoffline**が0以外の値に設定されている場合、WHEA は、ECC メモリページなどのハードウェアコンポーネントをオフラインにしません。 また、レジストリ値**Mempersistoffline**が0に設定されている場合、WHEA は、メモリページを BCD ストアに追加しません。 レジストリ値の詳細については、「 [WHEA ポリシー設定](whea-pfa-registry-settings.md)」を参照してください。



システムメモリマネージャーの詳細については、Windows SDK のドキュメントの「[メモリ管理](https://go.microsoft.com/fwlink/p/?linkid=140723)」を参照してください。


10. Windows カーネルは ETW イベントを生成し、エラー情報をシステムイベントログに記録します。








