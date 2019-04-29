---
title: Microsoft STI と Microsoft WIA の概要
description: Microsoft STI と Microsoft WIA の概要
ms.assetid: c973f9a2-48a5-420f-b317-0797171cf714
ms.date: 07/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: ef11d4821c786cccb6725049e8a0819e6c95be4e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392642"
---
# <a name="overview-of-microsoft-sti-and-microsoft-wia"></a>Microsoft STI と Microsoft WIA の概要

従来の Windows オペレーティング システムのイメージのアーキテクチャでは、ハードウェアの低レベルの抽象化、STI と高度な一連の TWAIN と呼ばれる Api を行いました。 最新の Windows オペレーティング システムでは、マイクロソフトは、Windows Imaging アーキテクチャ (WIA)、STI 上に構築されるイメージのアーキテクチャを使用します。 次の図は、これら 2 つのイメージのアーキテクチャを示しています。

![twain を示す図/sti と、microsoft のアーキテクチャをイメージング wia](images/sti-wia.png)

TWAIN、前の図に示すように/STI アーキテクチャには、TWAIN、画像を取得 STI、低レベル ハードウェア抽象化と共に、Api の大まかなセットが含まれています。 WIA アーキテクチャでは、イメージング デバイス Ihv に完全なソリューションを提供する基盤と STI が組み込まれています。

### <a name="differences-between-sti-and-wia"></a>STI と WIA の違い

WIA ドライバーでは、STI によって提供される基盤にビルドし、ために加えて、独自の STI インターフェイスを公開します。 少なくとも、WIA ドライバーが公開する必要があります、 **IStiUSD**インターフェイス。 STI には、任意の WIA インターフェイスに対応する依存関係はありません。 WIA ミニドライバーは、STI ミニドライバーに準拠する必要があります、ためには、WIA 対応のカメラまたはスキャナー、STI イメージ デバイスを STI ミニドライバーを記述すること勧めします。 ただし、ユーザー エクスペリエンスを向上させる WIA がお勧めします。 たとえば、カメラ、STI ドライバーは、エクスプ ローラーで縮小表示を示しません。

いくつかの違いは、STI と WIA を以下に示します。

-   STI はクライアント アプリケーションのプロセスとシステム サービス プロセスの両方で実行されます。System サービスのプロセスだけで、WIA が実行されます。

-   STI、ハードウェアの低レベルの抽象化されている必要がありますの詳細情報が、デバイスに関する; を操作するにはこのようなデバイスの詳細な情報がない WIA を操作できます。

-   STI でない完全なイメージング インターフェイスです。WIA、STI の上に構築されたは、イメージング ihv 向けの完全なソリューションです。 UI の IHV が指定したモジュールを (たとえば、Twain、) にのみ、デバイスの通信メカニズムを持って、UI フロント エンドを持たないため、STI アーキテクチャが必要です。 WIA ミニドライバーでは、既定値 (スキャナーとカメラ ウィザード) の UI があるため、独自の UI モジュールは必要ありません。 さらに、Twain インターフェイスは、WIA アーキテクチャでは、TWAIN 互換性レイヤーを通じてサポートされます。 Ihv は、拡張または WIA でこれらの既定 Ui を変更できます。

WIA アーキテクチャの詳細については、次を参照してください。 [WIA アーキテクチャの概要](wia-architecture-overview.md)します。

 

 




