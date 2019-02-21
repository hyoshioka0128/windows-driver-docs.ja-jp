---
title: PNPCPU 一般的なセッション
description: PNPCPU 一般的なセッション
ms.assetid: d0c1b6aa-fe23-4d01-aecf-897aba3672c9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b385dd4a84415d30c9178e0f88a62548ed63067a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553052"
---
# <a name="pnpcpu-typical-session"></a>PNPCPU 一般的なセッション


実行すると、 **-インストール**PNPCPU は、次のコマンドします。

-   バスの列挙子のドライバーをインストールします。

-   28 - デバイス マネージャーに表示される問題のコードで既存のすべてのプロセッサをマークします。

-   ブート構成データ (BCD) 設定を ONECPU を追加します。

-   Windows を使用しているときに、プロセッサの数を保存します **-インストール**を実行します。

-   プロセッサのドライバーの INF ファイルをあらかじめインストールします。

インストールが完了した後、次のメッセージが表示されます。

```
Enabled hot add cpu...
Please reboot the system before proceeding with the test
```

いずれか、コマンドラインからまたはシステムのメニュー オプションから、シャット ダウンを実行することによって、システムを再起動します。

お使いのコンピューターを再起動した後は、Windows が 1 つの論理プロセッサを使用してのみされます。 確認できますこのデバイス マネージャーでエラー コード 28 でプロセッサを検索して特定します。

 

 





