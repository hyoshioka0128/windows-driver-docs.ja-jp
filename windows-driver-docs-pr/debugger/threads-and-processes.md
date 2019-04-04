---
title: スレッドとプロセス
description: スレッドとプロセス
ms.assetid: 7ba8226c-3fb3-4ed6-8f87-69a7999e34ad
keywords:
- デバッガーのエンジン、スレッドおよびプロセス
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 542611a320b70611dba3be2d7a12db44b245cd1c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558342"
---
# <a name="threads-and-processes"></a>スレッドとプロセス


### <a name="span-idterminologyspanspan-idterminologyspanterminology"></a><span id="terminology"></span><span id="TERMINOLOGY"></span>用語集

スレッドとプロセスの概念はユーザー モードのデバッグとカーネル モード デバッグの間で異なります。

-   *ユーザー モードのデバッグ*、*プロセス*はオペレーティング システム プロセスです。 および*スレッド*は、オペレーティング システム スレッドです。

-   *カーネル モードのデバッグ*、[デバッガー エンジン](introduction.md#debugger-engine)作成、*仮想プロセス*; ターゲットごとに、このプロセスはカーネルを表し、いずれかに対応していませんオペレーティング システム プロセスです。 デバッガーは、作成対象のコンピューターでの物理プロセッサごとに、*仮想スレッド*; これらのスレッドがプロセッサを表すし、オペレーティング システム スレッドに対応していません。

イベントの発生時に、エンジンは、設定、*イベント処理*と*イベント スレッド*プロセスおよびスレッドに (オペレーティング システムまたは仮想)、イベントが発生しました。

*現在のスレッド*スレッド (オペレーティング システムまたは仮想)、エンジンが現在制御しています。 *現在のプロセス*プロセス (オペレーティング システムまたは仮想)、エンジンが現在制御しています。 イベントの発生時に、現在のスレッドとプロセスに初期設定されますイベント スレッドとプロセス;しかし、セッションがアクセス可能なときに、クライアントを使用して変更できます。

カーネル モードで、デバッガーは、暗黙的なプロセスと暗黙的なスレッドの追跡を保持します。 *暗黙的なプロセス*は仮想から物理メモリ アドレスへの変換を決定する、オペレーティング システム プロセスです。

*暗黙的なスレッド*コール スタック、スタック フレームでは、命令のオフセットなどのターゲットのレジスタを決定するオペレーティング システム スレッドです。

イベントの発生時に、暗黙的なスレッドと暗黙的なプロセスに初期設定されますイベント スレッドとプロセス;セッションのアクセス中に変更できます。

### <a name="span-idthreadandprocessdataspanspan-idthreadandprocessdataspanthread-and-process-data"></a><span id="thread_and_process_data"></span><span id="THREAD_AND_PROCESS_DATA"></span>スレッドおよびプロセスのデータ

エンジンは、いくつかのスレッドおよびプロセスに関する情報を保持します。 ターゲットのメモリにシステム スレッドとプロセス ID とシステムのハンドルと、プロセスの環境 (PEB)、スレッド環境ブロック (終了、およびその場所が含まれます。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

スレッドおよびプロセスの使用に関する詳細については、[を制御するスレッドとプロセス](controlling-threads-and-processes.md)を参照してください。

 

 





