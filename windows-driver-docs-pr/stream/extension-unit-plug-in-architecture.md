---
title: 拡張ユニット プラグインのアーキテクチャ
description: 拡張ユニット プラグインのアーキテクチャ
ms.assetid: cf2b32dd-0b65-41ce-b6e8-a9068e232600
keywords:
- 拡張機能ユニット WDK USB ビデオ クラスのアーキテクチャ
- WDK USB ビデオ クラスを制御する拡張ユニット
- レジストリ WDK USB ビデオ クラス
- WDK USB ビデオ クラスのイベント
- COM API の WDK USB ビデオ クラス
- プラグイン DLL WDK USB ビデオ クラス
- 拡張ユニット
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9c7985c2bf5c698dc6715242b219d7e8ba8ffc4e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384099"
---
# <a name="extension-unit-plug-in-architecture"></a>拡張ユニット プラグインのアーキテクチャ


USB ビデオ クラス ドライバーは、USB ビデオ KS プロキシ フィルター内のノードとして単位の拡張機能を公開します。 単位の拡張機能のコントロールがユーザー モードで KSNODETYPE 型のノードで、設定のプロパティとしてさらに公開される\_DEV\_特定します。 プロパティ セットの GUID では、拡張機能ユニット記述子の GUID と一致します。

個々 の単位の拡張機能コントロールする必要がある継続的に番号が付けられて 1 にはいくつかの最大値*n*します。 これらのコントロールは、単位の拡張機能プロパティを設定するには、プロパティ識別子 (Id) に直接マップし、を通じて標準 KSPROPERTY 要求を使用してアクセスできる[IKsControl](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksproxy/nn-ksproxy-ikscontrol)します。

アプリケーションからプロパティの要求に応答してでは、UVC ドライバーを持つプロパティ値を返します、 **MembersFlags**のメンバー、 [ **KSPROPERTY\_MEMBERSHEADER** 。](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksproperty_membersheader) KSPROPERTY にのみ設定\_メンバー\_範囲します。 UVC では階段状のサポート範囲にないデータまたは任意の長さの拡張機能単位の既定値。

アプリケーション単位の拡張機能プロパティを公開するには、COM API を公開するユーザー モードのプラグイン DLL を作成できます。 この API を実装するには、KS プロパティを使用して、設定に要求を行うことによって、 **IKsControl**インターフェイス。 *Vidcap.ax*特定のレジストリ エントリに基づくプラグイン ノード インターフェイスを自動的に読み込まれます。 アプリケーションは、インターフェイスを使用してアクセスして**IKsTopologyInfo::CreateNodeInstance**への呼び出しに続く**QueryInterface**で必要な COM API を取得するノード オブジェクト。

作成して、拡張ユニット プラグインを使用して、次の要素が必要です。

- IKsNodeControl という名前の拡張機能単位の API とインターフェイスを実装するヘッダーと cpp ファイル。 Vidcap.ax では、IKsNodeControl インターフェイスを使用して、プラグインの拡張機能ノードの識別子の通知を IKsControl のインスタンスを指定します。 サンプル コードでこれらのファイルが見つかります[サンプル拡張ユニット プラグイン DLL](sample-extension-unit-plug-in-dll.md)します。

- *.Rgs* ノードのインターフェイスとクラス Id (Clsid) を登録するファイル、 **HKLM\\システム\\CCS\\コントロール\\NodeInterfaces\\** <em>プロパティ\_設定\_GUID</em>レジストリ サブキー。 このレジストリ サブキー内のエントリには、インターフェイス ID (IID) および CLSID のバイナリ値が含まれます。 詳細については、次を参照してください。 [UVC 拡張機能のユニットのレジストリ エントリをサンプル](sample-registry-entry-for-uvc-extension-units.md)します。

- このインターフェイスを起動するアプリケーション。 アプリケーションはまず、IKsTopologyInfo::CreateNodeInstance を使用して、適切なノード ID とノードのインスタンスを作成します。 その後、アプリケーションを呼び出す**QueryInterface**要求単位の拡張機能インターフェイスを取得するノードのインスタンスにします。 詳細については、次を参照してください[UVC 拡張機能の単位用のサンプル アプリケーション](sample-application-for-uvc-extension-units.md)と[単位の拡張機能での自動更新イベントのサポート。](supporting-autoupdate-events-with-extension-units.md)

このセクションのコード例は、これらすべての要素を示しています。 参照してください[単位の拡張機能サンプル コントロールを作成](building-the-extension-unit-sample-control.md)にサンプルのプラグインと関連付けられているサンプル アプリケーション コードをビルドする方法について説明します。

プラグインの DLL が登録されているし、上記のレジストリ エントリが提供される、Vidcap.ax でノードのインスタンスが作成されると、関連するノードのインターフェイスが自動的に読み込まれます。

**注**  単位の拡張機能プロパティのセットは時点で、Windows XP SP2、およびフィルターではなく、ノードでのみサポートされています。

 

### <a name="registry-considerations"></a>レジストリの考慮事項

IID および CLSID のプラグインによってエクスポートされたインターフェイスを登録するには、DLL の登録やデバイスに固有のセットアップ情報 (INF) ファイルを使用できます。

参照してください[UVC 拡張機能のユニットのレジストリ エントリをサンプル](sample-registry-entry-for-uvc-extension-units.md)サンプルについては、 *.rgs*レジストリ エントリに必要な値を表示するファイル。 このトピックでは、USB ビデオ デバイスをインストールして、プラグインの DLL を登録するデバイス固有 INF ファイルを作成する方法も示します。 DLL の登録または特定のニーズに基づいて、デバイス固有の INF ファイルのいずれかを特定できます。

### <a name="schematic"></a>概略図

次のような回路図の記述と、拡張ユニット プラグインの使用に関連するさまざまなモジュール間のリレーションシップを示します。 具体的には、ドライバー、プラグインの DLL をアプリケーションからの接続をトレースし、最後に、デバイス自体の拡張機能単位にします。 回路図は、; 関係するさまざまな Guid も示されています。一致する色を使用して、同一の値が強調表示されます。

![拡張ユニット プラグインと関連付けられているモジュールを示す図](images/usbvidextension.gif)

### <a name="eventing-mechanisms"></a>イベント処理メカニズム

USB ビデオ クラスには、デバイスがそのコントロールのいずれかの変更のホスト ドライバーを通知、自動更新イベントがサポートしています。 Microsoft USB ビデオ クラス ドライバーは、アプリケーションの自動更新イベントが登録できるようにすることで、この概念をサポートします。 更新プログラムを取得するプロセスでは、次の 3 つの手順があります。

1.  使用して、更新イベントの登録[KSEVENTSETID\_VIDCAPNotify](https://docs.microsoft.com/windows-hardware/drivers/stream/kseventsetid-vidcapnotify)::[**KSEVENT\_しました\_自動\_更新**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksevent-vidcap-auto-update)

2.  イベント通知のイベント ハンドルをリッスンしてください。

3.  完了の通知をキャンセル

 

 




