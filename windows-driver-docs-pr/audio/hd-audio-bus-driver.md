---
title: HD オーディオ バス ドライバー
description: HD オーディオ バス ドライバー
ms.assetid: a08f4304-467b-45cf-8026-87f41b408692
keywords:
- HD オーディオ、ユニバーサルオーディオアーキテクチャ
- High Definition Audio (HD audio)、ユニバーサルオーディオアーキテクチャ
- UAA WDK
- ユニバーサルオーディオアーキテクチャ (WDK)
- バスドライバー WDK オーディオ
- HD オーディオ、バスドライバー
- High Definition Audio (HD audio)、bus driver
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6885db4038e3dedc0e7f53cccbe914b4ef6820ad
ms.sourcegitcommit: 98930ca95b9adbb6e5e472f89e91ab084e67e31d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/08/2020
ms.locfileid: "82925585"
---
# <a name="hd-audio-bus-driver"></a>HD オーディオ バス ドライバー


Hd オーディオバスドライバーは、HD オーディオバスインターフェイスコントローラーのハードウェアレジスタに直接アクセスする唯一のソフトウェアコンポーネントです。 バスドライバーは、その子である、オーディオとモデムのコーデックを制御する関数ドライバーのインスタンスである HD audio DDI を公開します。これは、HD オーディオコントローラーハードウェアのプログラミングに使用できます。 さらに、バスドライバーは、DMA エンジンとバス帯域幅を含む HD audio Link ハードウェアリソースを管理します。 関数ドライバーは、HD Audio DDI を通じてこれらのリソースを割り当て、解放します。

HD オーディオバスドライバー:

-   バス上のコーデックに対してクエリを行い、コーデックを管理する子を作成します。

-   要求されていない応答の割り込みサービスルーチン (Isr) を処理し、要求されていない応答をその子に伝達します。

-   子からコーデックにコマンドを渡し、コーデックから応答を取得します。

-   循環バッファーとの間でデータを転送する DMA エンジンを設定します。

-   HD オーディオリンクのバス帯域幅リソースを管理します。

-   ウォールクロックレジスタおよびリンク位置レジスタへのアクセスを提供します。

-   ストリームのグループの同期された開始と停止を提供します。

HD オーディオバスドライバーでは、次の機能が提供されません。

-   Intel High Definition Audio 仕様で定義されていない DSP または追加レジスタをプログラミングするためのインターフェイス。

-   優先順位の管理。

デバイスの列挙中に、hd オーディオバスドライバーは、hd オーディオコントローラーの HD オーディオリンクに接続されているコーデックを検出します。 コーデックごとに、コーデック内で検出された関数グループごとに1つの関数ドライバー (使用可能な場合) を読み込みます。 関数グループの詳細については、intel [HD audio](https://www.intel.com/content/www/us/en/standards/intel-standards-and-initiatives.html) web サイトの「Intel High Definition audio Specification」を参照してください。

 

 




