---
title: Windows のデバイスのためのドライバーの選択方法
description: Windows のデバイスのためのドライバーの選択方法
ms.assetid: 4c193b97-7b70-425f-99f2-ba976a4cc40a
keywords:
- ドライバーの選択, WDK デバイスのインストール, デバイスのセットアップの検索場所
ms.date: 03/02/2020
ms.localizationpriority: High
ms.openlocfilehash: 6dcd25c57c9f9625a77987a23822c049c4546c73
ms.sourcegitcommit: e1cfed28850a8208ea27e7a6a336de88c48e9948
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "79437059"
---
# <a name="how-windows-selects-a-driver-for-a-device"></a>Windows のデバイスのためのドライバーの選択方法


デバイスを接続する場合、Windows は、対応するデバイス ドライバーを検出してインストールする必要があります。

Windows 10 では、この照合プロセスが 2 つのフェーズに分けて行われます。 まず、Windows 10 は、最適なドライバーを[ドライバー ストア](driver-store.md)にインストールして、デバイスがすぐに操作を開始できるようにします。 そのドライバーをインストールした後、Windows 10 はさらに次の操作を行います。

* 一致する[ドライバー パッケージ](driver-packages.md)を Windows Update からダウンロードして、[ドライバー ストア](driver-store.md)に格納します。
* **DevicePath** レジストリ値で指定された場所に事前に読み込まれたドライバー パッケージを検索します。  **DevicePath** レジストリ値は、`HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion` サブキー下にあります。  既定では、**DevicePath** の値は、%SystemRoot%\\INF ディレクトリを指定します。

Windows 10 では、これらの場所で、最初にインストールされたドライバー パッケージよりもさらに適切なパッケージが見つかると、ドライバー ストアからインストールされたドライバーを、そのより適切なドライバーに置き換えます。

Windows 8 より以前の Windows バージョンの場合、ドライバーの照合プロセスでは、指定されている場合のみ **DevicePath** を調べ、それ以外の場合は、Windows Update を既定値とします。

次の表では、上記の説明を簡単にまとめています。

|検索フェーズ|Windows 7 の照合順序|Windows 8、Windows 10 の照合順序|
|--- |--- |--- |
|ドライバーをインストールする前|**DevicePath**、Windows Update、[ドライバー ストア](driver-store.md)|[ドライバー ストア](driver-store.md)|
|最初のドライバーを選択した後|適用できません|**DevicePath**、Windows Update|


> [!NOTE]
> Windows 10 バージョン 1709 以降では、Windows により、最適なドライバーが提供されますが、これは必ずしも最新のドライバーとは限りません。 ドライバーの選択プロセスでは、ハードウェア ID、日付およびバージョン、重要、自動、オプションのカテゴリが考慮されます。 Windows では、重要または自動のドライバーが最優先されます。 一致するドライバーが見つからない場合、WU は次にオプションのドライバーを検索します。 その結果、他の値は同じである古い重要なドライバーが、新しいオプションのドライバーよりも優先されます。


