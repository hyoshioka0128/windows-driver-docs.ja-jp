---
title: 拡張ユニット プラグインのアーキテクチャ
description: 拡張ユニット プラグインのアーキテクチャ
ms.assetid: cf2b32dd-0b65-41ce-b6e8-a9068e232600
keywords:
- 拡張機能ユニット WDK USB ビデオクラス、アーキテクチャ
- 拡張機能ユニットコントロール WDK USB ビデオクラス
- レジストリ WDK USB ビデオクラス
- イベント WDK USB ビデオクラス
- COM API WDK USB ビデオクラス
- プラグイン DLL WDK USB ビデオクラス
- 拡張機能ユニット
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1585baa20a0d2869d5026aeab26cc14c1544c1ee
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834405"
---
# <a name="extension-unit-plug-in-architecture"></a>拡張ユニット プラグインのアーキテクチャ


USB ビデオクラスドライバーは、拡張ユニットを USB Video KS プロキシフィルタのノードとして公開します。 拡張機能ユニットコントロールは、ノードに設定されたプロパティとして、ユーザーモードでさらに公開されます。これは、KSNODETYPE\_DEV\_固有の型です。 プロパティセットの GUID は、拡張機能の単位記述子の GUID と一致します。

個々の拡張機能ユニットコントロールは、1から最大値*n*まで連続して番号が付けられている必要があります。 これらのコントロールは、拡張機能のプロパティセットのプロパティ識別子 (IDs) に直接マップされ、 [Iksk コントロール](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksproxy/nn-ksproxy-ikscontrol)を介して標準の ksk プロパティ要求を使用してアクセスできます。

アプリケーションからのプロパティ要求に応答して、UVC ドライバーは、ksk プロパティの**Membersflags**メンバーを持つプロパティ値を返します。 [ **\_membersflags**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksproperty_membersheader)構造体は、ksk プロパティ\_メンバーに排他的に設定され\_キャスト. UVC では、任意の長さの、階段状の範囲や拡張単位の既定値はサポートされません。

拡張機能のプロパティをアプリケーションに公開するには、COM API を公開するユーザーモードのプラグイン DLL を記述します。 この API を実装するには、 **Ikscontrol**インターフェイスを使用して、KS プロパティセットに対して要求を行います。 *Vidcap.ax*は、特定のレジストリエントリに基づいてノードインターフェイスプラグインを自動的に読み込みます。 アプリケーションは、 **IKsTopologyInfo:: Creat Deinstance**の後に node オブジェクトで**QueryInterface**を呼び出して必要な COM API を取得することによって、インターフェイスにアクセスできます。

拡張機能単体プラグインを記述して使用するには、次の要素が必要です。

- 拡張機能の単体 API と IKsNodeControl という名前のインターフェイスを実装するヘッダーと cpp ファイル。 Vidcap.ax は IKsNodeControl インターフェイスを使用して、拡張ノード識別子のプラグインを通知し、Iksk コントロールのインスタンスを提供します。 これらのファイルのサンプルコードは、「[サンプルの拡張機能単体プラグイン DLL](sample-extension-unit-plug-in-dll.md)」に記載されています。

- HKLM\\システムの下にノードインターフェイスとクラス Id (Clsid) を登録する *.rgs*ファイル **\\CCS\\コントロール\\nodeinterfaces\\** <em>プロパティ\_GUID</em>レジストリサブキーを設定します。 このレジストリサブキーのエントリには、インターフェイス ID (IID) と CLSID のバイナリ値が含まれています。 詳細については、「 [UVC 拡張機能ユニットのサンプルレジストリエントリ](sample-registry-entry-for-uvc-extension-units.md)」を参照してください。

- このインターフェイスを呼び出すアプリケーション。 アプリケーションでは、最初に IKsTopologyInfo:: Creat Deinstance を使用して、正しいノード ID を持つノードインスタンスを作成します。 次に、アプリケーションはノードインスタンスで**QueryInterface**を呼び出して、必要な拡張機能の単位インターフェイスを取得します。 詳細については、「 [UVC 拡張機能ユニットのサンプルアプリケーション](sample-application-for-uvc-extension-units.md)」および「[拡張機能ユニットを使用した自動更新イベントのサポート](supporting-autoupdate-events-with-extension-units.md)」を参照してください。

このセクションのコード例では、これらのすべての要素について説明します。 サンプルプラグインと関連付けられているサンプルアプリケーションコードをビルドする方法については[、「拡張機能単体サンプルコントロールの](building-the-extension-unit-sample-control.md)ビルド」を参照してください。

プラグイン DLL が登録され、上記で説明したレジストリエントリが提供されると、Vidcap.ax はノードインスタンスの作成時に関連するノードインターフェイスを自動的に読み込みます。

**注**   Windows XP SP2 以降では、拡張機能のプロパティセットは、フィルターではなく、ノードでのみサポートされています。

 

### <a name="registry-considerations"></a>レジストリに関する考慮事項

プラグインによってエクスポートされたインターフェイスの IID と CLSID を登録するには、DLL の登録またはデバイス固有のセットアップ情報 (INF) ファイルを使用できます。

レジストリエントリに必要な値を示すサンプルの *.rgs*ファイルについては、「 [Uvc 拡張機能のサンプルレジストリエントリ](sample-registry-entry-for-uvc-extension-units.md)」を参照してください。 このトピックでは、デバイス固有の INF ファイルを作成して USB ビデオデバイスをインストールし、プラグイン DLL を登録する方法についても説明します。 特定のニーズに応じて、DLL の登録またはデバイス固有の INF ファイルのいずれかを選択できます。

### <a name="schematic"></a>配線

次の概略図は、拡張機能単体プラグインの作成と使用に関係するさまざまなモジュール間の関係を示しています。 特に、アプリケーションからプラグイン DLL への接続をドライバーに対してトレースし、最後にデバイス自体の拡張ユニットにトレースします。 このスケマティックは、関連するさまざまな Guid も示しています。一致する色を使用すると、同じ値が強調表示されます。

![拡張機能単体プラグインと関連モジュールを示す図](images/usbvidextension.gif)

### <a name="eventing-mechanisms"></a>イベントメカニズム

USB ビデオクラスでは、自動更新イベントがサポートされています。このイベントでは、デバイスは、そのコントロールの変更をホストドライバーに通知します。 Microsoft USB Video Class driver は、アプリケーションが自動更新イベントに登録できるようにすることで、この概念をサポートしています。 更新プログラムを取得するプロセスには、次の3つの手順が含まれます。

1.  [KSEVENTSETID\_VIDCAPNotify](https://docs.microsoft.com/windows-hardware/drivers/stream/kseventsetid-vidcapnotify):: KSEVENT\_VIDCAP を使用した更新イベントの登録[ **\_自動\_更新**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksevent-vidcap-auto-update)

2.  Notify イベントハンドルでイベントをリッスンしています

3.  完了したら通知をキャンセルする

 

 




