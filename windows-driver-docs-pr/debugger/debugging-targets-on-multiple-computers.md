---
title: 複数のコンピューター上のターゲットのデバッグ
description: 複数のコンピューター上のターゲットのデバッグ
ms.assetid: 3c4fa2d9-1443-4460-b570-9415a3600393
keywords:
- 複数のコンピューターのデバッグ
- システムでは、複数のコンピューター上のターゲット
- リモート デバッグ、複数のコンピューター
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 90b6fb0725150b2cf8e317169a2fea2beb9508b3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350569"
---
# <a name="debugging-targets-on-multiple-computers"></a>複数のコンピューター上のターゲットのデバッグ


## <span id="ddk_debugging_targets_on_multiple_computers_dbg"></span><span id="DDK_DEBUGGING_TARGETS_ON_MULTIPLE_COMPUTERS_DBG"></span>


デバッガーでは、複数のダンプ ファイルをデバッグしたり、ユーザー モード アプリケーションを同時にライブすることができます。 参照してください[複数のターゲットのデバッグ](debugging-multiple-targets.md)詳細についてはします。

さまざまなシステム上のプロセスがある場合でも、複数のライブ ターゲットをデバッグできます。 各システムでは、単にプロセス サーバーを起動し、使用、 **-premote**パラメーター [ **.attach (プロセスにアタッチ)** ](-attach--attach-to-process-.md)または[**します。(プロセスの作成) を作成する**](-create--create-process-.md)適切なプロセス サーバーを識別します。

*現在*または*active*は現在デバッグ中のシステムです。 使用する場合、 **.attach**または**に関する**コマンドを指定せずにもう一度、 **-premote**パラメーター、デバッガーは、アタッチまたは現在のシステム上のプロセスを作成します。

このようなデバッグ セッションを制御する方法の詳細については、次を参照してください。[複数のターゲットのデバッグ](debugging-multiple-targets.md)します。

 

 





