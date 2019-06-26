---
title: AVStream のスプリッター
description: AVStream のスプリッター
ms.assetid: c2cfc183-0f4c-4104-a580-234e0483eee4
keywords:
- WDK AVStream のスプリッター
- AVStream スプリッター WDK
- WDK AVStream のストリーム データの分割
- KSPIN_FLAG_SPLITTER
- 自動 WDK AVStream の分割
- 入力ピンの WDK AVStream の分割
- 出力ピン スプリッターの WDK AVStream の処理
- WDK AVStream の分割をピン留め
- プロセスが WDK AVStream をピン留め
- WDK AVStream フレーム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d2354cda1b30f70a4b52803a515e927d99597e2f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386699"
---
# <a name="avstream-splitters"></a>AVStream のスプリッター





AVStream、ミニドライバーは、ストリームが与えられた暗証番号 (pin) を通過すると、複数のコピーにデータ ストリームを分割するのに AVStream クラス ドライバーの機能を使用できます。 この分割プロセスは、2 つの同一の出力ストリームを生成するために、入力ストリームをコピーするには、ドライバーが必要な場合に役立ちます。

これを行うには、設定 KSPIN\_フラグ\_スプリッター、**フラグ**の暗証番号 (pin) のメンバー [ **KSPIN\_記述子\_EX** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_kspin_descriptor_ex)構造体。 このフラグがピンに設定されている場合、暗証番号 (pin) は、自動分割として機能します。 AVStream は自動的にストリームを分割するために必要なすべてのデータをコピーします。

DirectX8.0、KSPIN より後のリリースで\_フラグ\_スプリッター フラグがピンの両方で動作[フィルターを中心とした](filter-centric-processing.md)と[暗証番号 (pin) を中心とした](pin-centric-processing.md)フィルター。 以前のリリースでは、フィルターを中心としたフィルターにピンに対してのみ、このフラグをサポートします。

次の図は、入力ピンが 2 つの出力ピンにストリームを分割するフィルターの構成を示します。 この出力ピンのダウン ストリームのフィルター データを変更する*インプレース*します。

![分割の出力ピンを avstream フィルターを示す図 ](images/split1.png)

フレームは、入力ピンに到着し、入力キューに配置されます。 ミニドライバーは、入力キューと元の暗証番号 (pin) の出力キューとのみ対話します。 AVStream は自動的に、2 番目のピンのキューに、最初の pin のキューからデータをコピーします。

わかりやすくするため、この図は表示されません、出力ピンにフレームを指定する方法。 出力ピンにフレームを指定するなどがあります、リクエスターと各キューに関連付けられたアロケーター パイプここに属しているとします。 または、フレームは、ダウン ストリームのフィルターからものがあります。

[ **KSFILTER\_ディスパッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_ksfilter_dispatch)ベンダーから提供されたへのポインターを指定する構造体をミニドライバー [ *AVStrMiniFilterProcess*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nc-ks-pfnksfilterprocess)コールバック ルーチン。 このコールバック ルーチンは、ミニドライバーがへのポインターを受け取る、 [ **KSPROCESSPIN\_索引**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_ksprocesspin_indexentry)構造体の配列を含む[ **KSPROCESSPIN** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_ksprocesspin)構造体以下のとおりです。

この図では、プロセスのピンの一覧の 2 つの出力ピンの間、ミニドライバーの区別を示します。

![プロセスの図は分割ピンが 2 つのテーブルをピン留め](images/splitppin1.png)

DB を指す、この図では、 **DelegateBranch**のメンバー、 [ **KSPROCESSPIN** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_ksprocesspin)構造と CS を指す、 **CopySource**メンバー。 両方の**DelegateBranch**と**CopySource**入力ピンと出力ピンを最初のメンバーは**NULL**します。 これは、ミニドライバーは、このピンのフレームを処理することを示します。

ただし、2 番目の出力ピンには、 **CopySource**ポイントが最初の出力ピンにバックアップを作成します。 これは、2 番目の出力ピンが最初の出力ピンから別のパイプであると AVStream は、2 番目の出力ピンのキューに最初の出力ピンのキューに配置されている任意のデータをコピー自動的にことを示します。

複雑な分割線の場合は、2 つの出力ピンが同一のパイプに組み込まれているときに発生します。 ミニドライバー含めることができます 2 つのスプリッター ベースの出力ピン同一のパイプなどのダウン ストリームのフィルターではこれらのピンから送信されたデータが変更されない限り、します。 出力ピンは読み取り専用と見なされますので、データは変更されません。両方のダウン ストリームのフィルターは、同じバッファーを受信します。

そうでないときに、データを変更スプリッターの暗証番号 (pin) に自動的にアタッチするダウン ストリームのフィルターのこともできます。

ここでは、フィルターのレイアウトは、分割の出力ピンの 3 つのインスタンスを含むフィルターを示しています。 次の図のような可能性があります。

![次の 3 つの分割の出力ピン、avstream フィルターを示す図 ](images/split2.png)

ダウン ストリームのフィルターでは、データが変更されないために、A と B のピンが同一のパイプに割り当てられています。ダウン ストリームのフィルター A と B が同じバッファー ポインターを受信します。

*ミニドライバーは、入力キューと 1 つの出力キューとのみ対話します。* AVStream は A から自動的にコピー/キューの B と C キュー。 また、同じデータ フレームからピン A と B のピン (ストリーム ヘッダーが異なることに注意してください) を送信するスプリッター オブジェクトも作成します。

配列[ **KSPROCESSPIN** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_ksprocesspin)構造を次に示します。

![プロセスの図は次の 3 つの分割の出力ピンのテーブルをピン留め](images/splitppin2.png)

通常の状況で、ミニドライバーと対話する必要がありますのみの pin は暗証番号 (pin) A です。

上記の図を簡素化するには、要求者とアロケーターは、図から省略されました。 図は、プロセスの分割のフレームのみを示します。

 

 




