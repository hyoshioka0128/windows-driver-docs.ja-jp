---
title: IStream データ転送のドライバー変更
description: IStream データ転送のドライバー変更
ms.assetid: 1c837e4f-8d53-40ed-8f5b-0d525c7dd758
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 105646426418b2141044afd70c464e0a92751121
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570764"
---
# <a name="istream-data-transfer-driver-changes"></a>IStream データ転送のドライバー変更


Windows Vista より前に開発されたドライバーへの変更を最小限に抑えるには、ドライバーはありませんをサポートするために、新しいインターフェイスを実装する**IStream**データ転送。 代わりに、新しいインターフェイスはによって公開された、 [IWiaMiniDrvCallBack インターフェイス](https://msdn.microsoft.com/library/windows/hardware/ff543943)します。 ドライバーを呼び出すことができます**IWiaMiniDrvCallBack::QueryInterface**新しい**IWiaTransfer**がそれらにアクセスできるように、データ ストリームと状態の通知されるコールバック関数。 **IWiaTransfer**インターフェイスは、Microsoft Windows SDK ドキュメントで説明します。

すべての転送では、同様はないファイルまたはメモリの転送分岐ロジックで処理するため、ドライバー内部のデータ転送のコードはより単純なようになりました。

サポートしていないドライバー、 **IStream**転送モデルは通常、次の手順を実行します。

1.  要求がアップロードまたはダウンロードするのかを判断するフラグを確認します。

2.  取得、 [IWiaMiniDrvCallBack](https://msdn.microsoft.com/library/windows/hardware/ff543943)インターフェイス。

3.  コールバック関数からコピー先のストリームを受信します。

4.  データ転送のループを実行します。
    1.  デバイスからデータを受信します。
    2.  データ ストリームを書き込みます。

ただし、実装、新しいドライバーの**IStream**転送モデルでは、WIA サービスの呼び出しがない[ **IWiaMiniDrv::drvWriteItemProperties** ](https://msdn.microsoft.com/library/windows/hardware/ff545020)のため*フォルダー取得*はサポートされています。

フォルダーの取得で 1 つの転送要求は、親アイテムに対してが、実際のアイテム プロパティが転送されている子項目の各。 **IWiaMiniDrv::drvWriteItemProperties**デバイスの設定をプログラムにこのメソッドは使用できませんので、各子項目のメソッドが呼び出されません。 サポートするドライバーに対して**IStream**データ転送、サービス呼び出しで WIA [ **IWiaMiniDrv::drvAcquireItemData** ](https://msdn.microsoft.com/library/windows/hardware/ff543956)代わりにします。

**注**  この変更が新しいデータ転送をサポートするドライバーだけに影響します。 従来のドライバーがサポートされていない**IStream**データ転送の場合に影響しません。、WIA サービスの呼び出しは引き続き、 **IWiaMiniDrv::drvWriteItemProperties**それらのメソッド。

 

ドライバーが複数の呼び出しをフォルダーの買収**IWiaTransferCallback::GetNextStream** (これについては説明、Microsoft Windows SDK ドキュメントで)、ドライバーは、一度に 1 つだけアクティブなストリームことができます。

ドライバーのみ、ストリームを呼び出す必要があります**IStream::Write**、 **IStream::Seek**、および**IStream::SetSize**メソッド (これは、Windows SDK のドキュメントで説明しています)ダウンロード操作の実行中 この制限を簡単にフィルターを作成します。 ドライバーでは、コピー先のストリームが、他のメソッドを実装することは期待できません。

ときに、 [ **WIA\_DPS\_ページ\_サイズ**](https://msdn.microsoft.com/library/windows/hardware/ff551417)プロパティが WIA\_ページ\_自動 (つまり、ページの自動サイズ検出は、有効)、ドライバーは正確なディメンションについて情報イメージ イメージ データの転送が完了した後にのみ。 ストリーム ベースの転送では、ドライバーは、転送の最後にイメージ ヘッダーにイメージのサイズを更新する必要があります。 新しいセッション、WIA の値の先頭に\_DPS\_ページ\_サイズ プロパティは、WIA 以外の値に常に設定する必要があります\_ページ\_自動。

 

 




