---
title: WHEA によって実行される PFA
description: WHEA によって実行される PFA
ms.assetid: c93b15aa-9b99-4dfa-8c97-b503654e44f2
keywords:
- 予測エラー分析 (PFA) WDK WHEA、エラー修正コードメモリ
- PFA WDK WHEA、エラー修正コードのメモリ
- エラー修正コードメモリ WDK WHEA
- エラー修正コードメモリ WDK WHEA、予測エラー分析
- 低レベルのハードウェアエラーハンドラー WDK WHEA
- LLHEH WDK WHEA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0a234709a841f38fa2b9d5c77bf1d02dba113d81
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845633"
---
# <a name="pfa-performed-by-whea"></a>WHEA によって実行される PFA


Windows 7 以降では、Windows ハードウェアエラーアーキテクチャ (WHEA) は、エラー修正コード (ECC) メモリの予測エラー分析 (PFA) をサポートしています。

**重要**  [プラットフォーム固有のハードウェアエラードライバー (pshed) プラグイン](platform-specific-hardware-error-driver-plug-ins2.md)は、WHEA ではなく、ECC メモリで pshed を実行できます。 プラグインが PFA を実行する場合は、pfa[プラグインによって実行される pfa](pfa-performed-by-a-pshed-plug-in.md)に記載されている手順に従う必要があります。 プラグインは、このトピックで説明されている手順に従わないでください。

 

ECC メモリエラーが発生すると、WHEA は次の手順を実行します。

1.  *低レベルのハードウェアエラーハンドラー* (*LLHEH*) には、メモリエラー状態の有無が通知されます。

2.  LLHEH は、エラーソースからメモリエラー情報を取得し、エラーデータを使用してハードウェアエラーパケットを入力します。 このパケットは、 [WHEA\_エラー\_パケット](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff560465(v=vs.85))構造として書式設定されます。

3.  LLHEH は、プラットフォーム固有のハードウェアエラー情報を取得するために、を呼び出します。 がインストールされていて、エラーに関する情報を取得するように登録されている場合は、LLHEH に返されるエラー情報をプラグインが変更できるように、pshed プラグインが呼び出されます。

4.  LLHEH は、Windows オペレーティングシステムカーネルを呼び出して、エラーパケットを渡します。

5.  Windows カーネルは[エラーレコード](error-records.md)を作成し、LLHEH から受信したエラーパケットの情報を追加します。 さらに、Windows カーネルによって、エラーに関する他の情報 (エラーソース、エラーの重大度、エラーが発生した回数など) がエラーレコードに追加されます。

6.  Windows カーネルは、エラーレコードにセクションを追加できるようにするために、を呼び出します。

7.  エラーに関する情報を取得するために登録されているプラグインがインストールされている場合は、プラグインがエラーレコードの情報を変更できるように、pshed プラグインが呼び出されます。

    **注**  pshed プラグインが pshed を実行していない場合は、WHEA [ **\_エラー\_パケット\_フラグ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_whea_error_packet_flags)のメンバーである[whea\_error\_パケット](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff560465(v=vs.85))構造体のビットを設定しないようにする必要があります。

     

8.  PFA が有効になっている場合、WHEA は [ECC メモリ] ページで PFA を実行します。 このプロセスの詳細については、「 [WHEA が ECC メモリで PFA を実行する方法](how-whea-performs-pfa-on-ecc-memory.md)」を参照してください。

9.  Windows カーネルは ETW イベントを生成し、エラー情報をシステムイベントログに記録します。

 

 




