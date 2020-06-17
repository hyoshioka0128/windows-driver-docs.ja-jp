---
title: AVStream のテストとデバッグ
description: AVStream のテストとデバッグ
ms.assetid: 7a3eeeb5-1ff4-4110-9168-c716cd7776b8
keywords:
- AVStream WDK ストリーミングメディアのテスト
- AVStream WDK、テスト
- WDK AVStream のデバッグ
- AVStream WDK、デバッグ
- AMCap2
- GraphEdt
- KsStudio ユーティリティ
- MCStream
- UVCView
- アクティブなムービーキャプチャの WDK AVStream
- AVStream WDK、ツール
- Kernel Streaming Development Studio WDK AVStream
- マルチチャネルストリーミングツール WDK AVStream
- USB ビデオクラス記述子ビューアー WDK AVStream
ms.date: 06/16/2020
ms.localizationpriority: medium
ms.openlocfilehash: 4e71b904557b117ec73cfa96153803a7751c28b8
ms.sourcegitcommit: 97a8d24b1b48602e4ccaa63a113f7c8cdb0c6df5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/16/2020
ms.locfileid: "84812437"
---
# <a name="avstream-testing-and-debugging"></a>AVStream のテストとデバッグ

Windows 7 WDK 以降では、 *WDKPath \\ tools \\ avstream*フォルダー階層に3つのツールが用意されています。 このトピックでは、各ツールの目的と基本的な使用方法について説明します。 場合によっては、フォルダー階層に追加のドキュメントが含まれています。

## <a name="graphedt"></a>GraphEdt

*GraphEdt.exe*は、DirectShow アプリケーションプログラミングインターフェイスを使用して、機能的なマルチメディアフィルターグラフを視覚的に作成するための開発ツールです。

GraphEdt には、 *GraphEdt.exe* (アプリケーション)、 *GraphEdt* (ヘルプドキュメント)、および*Proppage.dll* (ヘルパーフィルター) という3つのバイナリコンポーネントが含まれています。 *Proppage.dll*は、コマンド "regsvr32 proppage.dll" を使用して、オペレーティングシステムに登録されている場合、フィルターの追加のプロパティ設定を公開します。 Regsvr32 コマンドは、昇格された特権レベルで実行する必要があります。

GraphEdt バイナリは、x86 ベースおよび x64 ベースのアーキテクチャ用に用意されています。 GraphEdt は、Microsoft Windows 2000、XP、Windows 2003 Server、Windows Vista、および Windows 7 で実行できます。

## <a name="ksstudio"></a>KsStudio

*KsStudio.exe* (Kernel Streaming development Studio) は、マルチメディアドライバーのプロパティ、pin、およびサポートされているメディアを調べるために使用される開発ツールです。

Windows 7 WDK には、x86 ベースおよび x64 ベースのアーキテクチャ用の KsStudio バイナリが含まれています。 また、XP フォルダーには Windows XP および Windows 2003 Server のバージョンがあります (x86 と x64 の両方)。 Windows 7 では、バイナリは*KsStudio.exe* (アプリケーション)、 *ksstudio .chm* (ヘルプドキュメント)、 *KsMon.sys* (ヘルパーデバイスドライバー) です。 XP および Windows 2003 Server の場合は、*ndAnlyz.dll* (ヘルパーファイル) もあります。

KsStudio はカーネル開発ツールであるため、慎重に使用する必要があります。 *KsStudio.exe*は、概要ログを開始ディレクトリに書き込む必要があります。このログには、ユーザーの書き込みアクセス権が必要です。 KsStudio は、ヘルパードライバー *KsMon.sys*の読み込みを試みます。 この読み込みは省略可能であり、 *KsMon.sys*が開始ディレクトリにあり、コマンドが昇格された特権レベルで実行されている場合にのみ成功します。 通常、KsStudio では、"KS Studio Filter Options" というタイトルのダイアログボックスが表示されます。これにより、ユーザーは、列挙するクラスであるパラメーターを指定できます。 そのダイアログボックスの [**クラス**] ボタンを使用して、none、any、または all クラスを選択します。

これは、マルチメディアデバイス作成者向けの、複雑で洗練された、非常に便利な開発ツールです。 詳細については、 *Ksstudio .chm*のヘルプファイルを参照してください。

## <a name="usbview"></a>USBView

*USBView.exe* (Usb ビデオクラス記述子ビューアー) は、ユーザーが接続されている任意の USB デバイスの記述子を調べることができるようにする開発ツールです。 USBView は、USB セクションでサンプルとして Windows Driver Kit (WDK) に付属しています。 USBView は、マルチメディア USB オーディオおよびビデオクラスデバイスの説明的な記述子情報を追加します。

> [!NOTE]
> Windows 7 WDK では、このツールには UVCView というタイトルが付いています。

USBView には、 *USBView.exe*というバイナリコンポーネントが1つ含まれています。 WDK では、この実行可能ファイルは*ツール \\ avstream*フォルダー階層に配置されます。 ドキュメントについては、 *WDKPath \\ src \\ usb \\ usbview*の usbview サンプルを参照してください。

Usb ビューバイナリは、x86 ベースおよび x64 ベースのアーキテクチャ用に用意されています。 USBView は、Microsoft Windows 2000、XP、Windows 2003 Server、Windows Vista、および Windows 7 で実行できます。

次のツールは、以前のバージョンの Windows で提供されており、Windows 7 以降では使用しないことをお勧めします。

## <a name="amcap2"></a>AMCap2

*AMCap2.exe* (アクティブなムービーキャプチャ) は、Microsoft DirectShow アプリケーションプログラミングインターフェイスを使用して、オーディオおよびビデオキャプチャデバイスを列挙して使用するためのアプリケーションです。

AMCap2 には、 *AMCap2.exe*というバイナリコンポーネントが1つ含まれています。

AMCap2 バイナリは、x86 ベースおよび x64 ベースのアーキテクチャ用に用意されています。 AMCap2 は、Microsoft Windows 2000、XP、Windows 2003 Server、および Vista で実行されます。

AMCap2 を初期化すると、デバイスメニューで利用可能なオーディオおよびビデオキャプチャデバイスが列挙されます。 [なし] または [1 つのオーディオまたはビデオデバイス] を選択できます。 [設定] メニューでは、特定のデバイス属性を選択できます。

詳細については、 [DirectShow のドキュメント](https://docs.microsoft.com/previous-versions//ms783323(v=vs.85))を参照してください。

*AMCap2.exe*ツールは、Windows SERVER 2008 wdk 以前のバージョンの wdk に表示されます。 このツールは、x86 ベースと x64 ベースの両方のプラットフォームで Windows 7 WDK から削除されています。

AMCap2 のすべての機能は、Windows 7 WDK に含まれる既存の GraphEdt ツールでも使用できます。

## <a name="mcstream"></a>MCStream

*MCStream.exe* (マルチチャネルストリーミングツール) は、ユーザーが複数のチャネルの wave トーンを生成して表示できるようにする開発ツールです。 MCStream は、DirectShow やメディアファンデーションではなく、KS を直接使用する従来のツールです。

> [!WARNING]
> MCStream は、すべてのオーディオレンダラーで動作するわけではありません。

MCStream には、 *MCStream.exe* (アプリケーション) と*MCStream.txt* (ヘルプドキュメント) という2つのバイナリコンポーネントが含まれています。

MCStream バイナリは、x86 ベースおよび x64 ベースのアーキテクチャ用に用意されています。 MCStream は、Microsoft Windows 2000、XP、Windows 2003 Server、および Vista で実行されます。

*MCstream.exe*ツールは、x86 ベースと x64 ベースの両方のプラットフォームで WINDOWS 7 WDK には含まれていません。

このツールでは、Windows 7 以降のオペレーティングシステムでのドライバーの開発には推奨されなくなった従来のテクノロジを使用します。
