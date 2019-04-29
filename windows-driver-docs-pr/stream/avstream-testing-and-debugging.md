---
title: AVStream のテストとデバッグ
description: AVStream のテストとデバッグ
ms.assetid: 7a3eeeb5-1ff4-4110-9168-c716cd7776b8
keywords:
- ストリーミング メディア AVStream WDK のテスト
- テストの AVStream WDK
- WDK AVStream のデバッグ
- AVStream WDK、デバッグ
- AMCap2
- GraphEdt
- KsStudio ユーティリティ
- MCStream
- UVCView
- アクティブなビデオ キャプチャ WDK AVStream
- AVStream WDK、ツール
- カーネル Development Studio の WDK AVStream のストリーミング
- マルチ チャネル ツール WDK AVStream のストリーミング
- USB ビデオ クラス記述子ビューアー WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6070f20dea1f73b5beafd05dba108cf5b3784b4a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392721"
---
# <a name="avstream-testing-and-debugging"></a>AVStream のテストとデバッグ


以降、Windows 7 の WDK では、3 つのツールがで提供される、 *WDKPath\\ツール\\avstream*フォルダー階層。 このトピックでは、目的と各ツールの基本的な使用方法について説明します。 場合によっては、その他のドキュメントは、フォルダー階層に含まれます。

### <a name="graphedt"></a>**GraphEdt**

*GraphEdt.exe*は DirectShow のアプリケーション プログラミング インターフェイスを使用してマルチ メディア機能のフィルターのグラフの視覚的に構築するための開発ツールです。

GraphEdt には、次の 3 つのバイナリ コンポーネントが含まれています。*GraphEdt.exe* (アプリケーション)、 *GraphEdt.chm* (ヘルプ ドキュメント) および*Proppage.dll* (ヘルパー フィルター)。 *Proppage.dll*コマンド"regsvr32 proppage.dll"を使用して、オペレーティング システムに登録されているときに、フィルターの追加のプロパティの設定を公開します。 Regsvr32 コマンドは、昇格された特権レベルで実行する必要があります。

GraphEdt バイナリは、x86 ベースおよび x64 ベースのアーキテクチャ用に提供されます。 GraphEdt は、Microsoft Windows 2000、XP、Windows Server 2003、Windows Vista、および Windows 7 で実行されます。

### <a name="ksstudio"></a>**KsStudio**

*KsStudio.exe* (カーネル ストリーミング Development Studio) は、開発ツールでマルチ メディアのドライバーのプロパティ、pin の確認に使用し、メディアをサポートします。

Windows 7 の WDK には、x86 ベースおよび x64 ベースのアーキテクチャ用 KsStudio バイナリが含まれています。 さらに、Windows XP および Windows 2003 サーバーが XP フォルダー (x86 と x64 の両方) のバージョンがあります。 バイナリは、Windows 7 では、 *KsStudio.exe* (アプリケーション)、 *KsStudio.chm* (ヘルプ ドキュメント) および*KsMon.sys* (ヘルパーのデバイス ドライバー)。 XP および Windows Server 2003 ではも S*ndAnlyz.dll* (ヘルパー ファイル)。

KsStudio、カーネルの開発ツールは、そのため、慎重に使用する必要があります。 *KsStudio.exe*開始のディレクトリは、ユーザーの書き込みアクセス権が必要に概要ログを書き込む必要があります。 そのヘルパー ドライバーの読み込みを試みます KsStudio *KsMon.sys*します。 この読み込みは省略可能であり、場合にのみ成功*KsMon.sys*開始ディレクトリでは、コマンドは、昇格された特権レベルで実行されているとします。 通常、KsStudio という「KS Studio フィルター オプション、」ユーザーが最も重要なものは、クラスを列挙するパラメーターを指定するダイアログ ボックスが表示されます。 使用して、**クラス**any が none を選択するには、そのダイアログ ボックスまたはすべてのクラスでボタンをクリックします。

これは、マルチ メディア デバイスの作成者が複雑でありまだ簡潔で洗練された、非常に便利な開発ツールです。 詳細についてを参照してください、 *KsStudio.chm*ヘルプ ファイル。

### <a href="" id="uvcview"></a>**USBView**

*USBView.exe* (USB ビデオ クラス記述子ビューアー) は、接続された USB デバイスの記述子を確認できる開発ツールです。 USBView では、USB のセクションでサンプルとして Windows Driver Kit (WDK) に付属しています。 USBView は、マルチ メディアの USB オーディオとビデオ クラス デバイスのわかりやすい記述子の情報を追加します。

**注**  Windows 7 WDK で、このツールは UVCView タイトルです。

 

USBView には、1 つのバイナリ コンポーネントが含まれています。*USBView.exe*します。 Wdk には、この実行可能ファイルにある、*ツール\\avstream*フォルダー階層。 ドキュメントについては、USBView サンプルを参照してください。 *WDKPath\\src\\usb\\usbview*します。

USBView バイナリは、x86 ベースおよび x64 ベースのアーキテクチャ用に提供されます。 Microsoft Windows 2000、XP、Windows Server 2003、Windows Vista、および Windows 7 で USBView が実行されます。

次のツールでは、以前のバージョンの Windows で提供され、Windows 7 以降の使用は推奨されません。

### <a name="amcap2"></a>**AMCap2**

*AMCap2.exe*を列挙すると、オーディオおよびビデオ キャプチャ デバイスを Microsoft DirectShow のアプリケーション プログラミング インターフェイスを使用して、アプリケーションは、(アクティブなビデオ キャプチャ) します。

AMCap2 には、1 つのバイナリ コンポーネントが含まれています。*AMCap2.exe*します。

AMCap2 バイナリは、x86 ベースおよび x64 ベースのアーキテクチャ用に提供されます。 AMCap2 は、Microsoft Windows 2000、XP、Windows Server 2003、および Vista で実行されます。

AMCap2 初期化すると、使用可能なオーディオとそのデバイス メニューにビデオ キャプチャ デバイスを列挙します。 None または 1 つのオーディオまたはビデオ デバイスを選択できます。 [設定] メニューには、特定のデバイス属性を選択できます。

詳細については、DirectShow、 [DirectShow ドキュメント](https://go.microsoft.com/fwlink/p/?linkid=68207)します。

*AMCap2.exe*ツール、Windows Server 2008 の WDK と以前のバージョンの WDK に表示されます。 このツールは x86 ベースし、x64 ベースの両方のプラットフォームの Windows 7 の WDK から削除されました。

AMCap2 のすべての機能は、Windows 7 の WDK に含まれている既存の GraphEdt ツールで引き続き使用できます。

### <a name="mcstream"></a>**MCStream**

*MCStream.exe* (マルチ チャネル ストリーム ツール) は、ユーザーを生成し、複数のチャネル wave トーンをレンダリングできる開発ツール。 MCStream は、DirectShow や Media Foundation ではなく、直接 KS を使用する古いツールです。

**警告**  MCStream はすべてのオーディオのレンダラーでは機能しません。

 

MCStream には、2 つのバイナリ コンポーネントが含まれています。*MCStream.exe* (アプリケーション) と*MCStream.txt* (ヘルプを参照)。

MCStream バイナリは、x86 ベースおよび x64 ベースのアーキテクチャ用に提供されます。 MCStream は、Microsoft Windows 2000、XP、Windows Server 2003、および Vista で実行されます。

*MCstream.exe*ツールは、x86 ベースし、x64 ベースの両方のプラットフォームの Windows 7 の WDK には含まれません。

このツールは、Windows 7 以降のオペレーティング システムでドライバーの開発には推奨されなくレガシ テクノロジを使用します。

 

 




