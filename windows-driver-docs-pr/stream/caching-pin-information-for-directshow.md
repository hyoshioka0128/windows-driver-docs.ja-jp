---
title: DirectShow のキャッシュの暗証番号 (pin) 情報
description: DirectShow のキャッシュの暗証番号 (pin) 情報
ms.assetid: 1e6a973b-32d2-4ac2-9cd6-f4d3c329cecf
keywords:
- 暗証番号 (pin) のデータ キャッシュ WDK BDA
- WDK AVStream をキャッシュします。
- DirectShow の暗証番号 (pin) のデータ キャッシュの WDK AVStream
- 更新の WDK AVStream 暗証番号 (pin) のデータ キャッシュ
- ドライバーのアーキテクチャの WDK AVStream、暗証番号 (pin) のデータ キャッシュのブロードキャストします。
- BDA WDK AVStream、暗証番号 (pin) のデータ キャッシュ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1f215ce1a0a39092dc180dc1e5390dd7a5a1a6f7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56561102"
---
# <a name="caching-pin-information-for-directshow"></a>DirectShow のキャッシュの暗証番号 (pin) 情報





アプリケーションは、DirectShow を使用できます**IFilterMapper2**を特定の条件を満たすフィルターを自動的に検索するインターフェイス。 このアプリケーションは、提案されたフィルターのリストを使用している**IFilterMapper2**自動的に受信してテレビ信号を表示するフィルターでフィルター グラフをビルドするを返します。 指定すると、条件を満たすフィルターをすばやく検索する**IFilterMapper2**キャッシュに以前に入力されたフィルターとその pin に関する情報を使用します。 次の段落の説明としては、このキャッシュを指す、*データ キャッシュをピン留め*します。

暗証番号 (pin) のデータ キャッシュ内に含まれる情報には、メディアと、フィルターを公開する各ピンのメディアの種類の一覧が含まれています。 **IFilterMapper2**グラフにあるフィルターで pin に使用可能なフィルターを接続できるかどうかを判断するこのキャッシュ情報を使用します。 この決定を行うと、フィルターへの接続が妨げられてこと中またはメディアの種類が一致しないためにの特定にのみ、フィルターのインスタンスを作成するオーバーヘッドがなくなります。 フィルターの暗証番号 (pin) のデータ キャッシュが最新ではない場合、フィルターをフィルター グラフ内の接続の候補として誤って排除します。

ミニドライバーの BDA コンポーネントの BDA フィルター インスタンスの暗証番号 (pin) 情報が正確にフィルターで公開されているように BDA ミニドライバーは、DirectShow を使用する pin データ キャッシュが最新ではないことを判断、ときにそのミニドライバーでは暗証番号 (pin) のデータ キャッシュを更新する必要があります。グラフ。 BDA ミニドライバーは、次のシナリオでの説明に従って、DirectShow の暗証番号 (pin) のデータ キャッシュを更新します。

-   BDA ミニドライバーは、必須、ミニドライバーは最初にそのミニドライバーがユーザー モードで DirectShow フィルターとして BDA フィルターを表示する方法に応じて BDA フィルターのインスタンスを作成するときに、DirectShow の暗証番号 (pin) のデータ キャッシュを更新することができない可能性があります。 BDA ミニドライバーの情報 (INF) ファイルには、ミニドライバーは、DirectShow フィルター BDA フィルターに使用するメカニズムを指定します。

    BDA ミニドライバーを使用して、通常、 [(KS) proxy モジュールのカーネル ストリーミング](https://msdn.microsoft.com/library/windows/hardware/ff560877)(*Ksproxy.ax*) DirectShow フィルター処理をフィルターするには、BDA を提示します。 KS プロキシは、これらのフィルターのインスタンスが最初に作成されるたびに、BDA フィルターの暗証番号 (pin) 情報を公開する DirectShow の暗証番号 (pin) のデータ キャッシュを自動的に更新します。 そのため、KS プロキシを使用する BDA ミニドライバーでは、最初に、フィルターのインスタンスを作成するときに、DirectShow の暗証番号 (pin) のデータ キャッシュを更新する操作を実行する必要はありません。 BDA フィルターが KS プロキシ経由のユーザー モードに公開されている場合は、キャッシュされた情報は、メディアを自動的に追加し、直後に、フィルターのフィルターのインスタンス上に存在するファクトリを暗証番号 (pin) のメディアの種類がディスパッチ ルーチンを返します。 を作成します。

    いくつか BDA ミニドライバーは、DirectShow フィルターとして BDA フィルターを提示するのに KS プロキシを使用することはしません。 たとえば、受信 BDA を実装する BDA 受信者ミニドライバーをフィルター処理またはアナログ テレビ信号の受信プロセスは、いずれかを使用、 *KSTVTune.ax*または*KSXBar.ax*モジュールとしてこれらの BDA フィルターを表示するにはDirectShow フィルター。 これらのモジュールは、DirectShow の暗証番号 (pin) のデータ キャッシュを更新する標準的な KS プロキシ インターフェイスのメソッドを使用しないので、BDA フィルターがこの種の BDA ミニドライバーは、ミニドライバーは、最初にフィルターのインスタンスを作成するとき DirectShow の暗証番号 (pin) のデータ キャッシュを更新する必要があります。 BDA ミニドライバーの呼び出しをこれらのフィルターのインスタンスを作成するときに、DirectShow の暗証番号 (pin) のデータ キャッシュが更新されることを確認するには、するには、 [ **BdaFilterFactoryUpdateCacheData** ](https://msdn.microsoft.com/library/windows/hardware/ff556455)呼び出した後すぐに関数[ **BdaInitFilter** ](https://msdn.microsoft.com/library/windows/hardware/ff556464)フィルターの実装内部の関数のディスパッチ ルーチンを作成します。 この呼び出しでは、ミニドライバーは、フィルターのすべての初期ピンを更新する pin 情報を渡します。

-   ピンを作成できます BDA フィルターを動的にフィルターのディスパッチの作成後ルーチンが完了します。 BDA フィルターの最初に作成されたインスタンスが BDA フィルターのテンプレートのトポロジに記載されているすべてのピンのインスタンスを公開しないかどうか ([**BDA\_フィルター\_テンプレート**](https://msdn.microsoft.com/library/windows/hardware/ff556523))、BDA ミニドライバーを呼び出す必要がありますし、 **BdaFilterFactoryUpdateCacheData**については、フィルターのテンプレートのトポロジで表示されているすべてのピンを強制的にします。

**注**  触れるし、レジストリが変更されために、更新 DirectShow の暗証番号 (pin) のデータ キャッシュが大きなオーバーヘッドです。 さらに、DirectShow の暗証番号 (pin) のデータ キャッシュを更新するには、DirectShow フィルター グラフを自動的にビルドするために必要な時間に影響します。 そのため、BDA ミニドライバーを呼び出す必要があります**BdaFilterFactoryUpdateCacheData** DirectShow を使用する pin データ キャッシュが最新ではないことを決定する場合にのみ可能なピンをすべて。

 

可能であれば、BDA ミニドライバーを呼び出す必要があります**BdaFilterFactoryUpdateCacheData**たびに、ドライバー、ファームウェア、またはハードウェアの更新が発生しました。

 

 




