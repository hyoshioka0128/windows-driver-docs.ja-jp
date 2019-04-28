---
title: Srcsrv.ini ファイル
description: Srcsrv.ini ファイル
ms.assetid: 5a3f5990-e43a-4c50-a16f-cbaa9f706ece
keywords:
- SrcSrv、Srcsrv.ini ファイル
- Srcsrv.ini ファイル
- SrcSrv、SRCSRV_INI_FILE 環境変数
- SRCSRV_INI_FILE 環境変数
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9c498cbf6e3856ed07dd9093ee997948303eaae8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365984"
---
# <a name="the-srcsrvini-file"></a>Srcsrv.ini ファイル


Srcsrv.ini ファイルは、すべてのソース管理サーバーのマスター リストです。 各エントリには、次の形式があります。

```ini
MYSERVER=ServerInfo
```

Perforce を使用する場合、 *ServerInfo*の後に、コロン、およびポート番号を使用して、サーバーの完全なネットワーク パスで構成されます。 例:

```ini
MYSERVER=machine.corp.company.com:1666
```

Srcsrv.ini は、実際にソースがこのパッケージに付属するモジュールを使用してビルドのインデックスを作成したら、必要なファイルです。 このエントリは、サーバーの情報を記述するために使用するエイリアスを作成します。 値は、サポートしているすべてのサーバーに対して一意でなければなりません。

このファイルは、デバッガーを実行しているコンピューターにもインストールできます。 SrcSrv の開始時に調べ Srcsrv.ini の値。これらの値は、.pdb ファイルに含まれる情報をオーバーライドします。 これにより、デバッグ時に、代替のソース管理サーバーを使用するデバッガーを構成できます。 ただしも、サーバーを管理してそれらの名前を変更していない場合があります必要はありません、クライアントのデバッガーのインストールでこのファイルをインクルードします。

このファイルは、クライアント側で他の目的でも機能します。 詳細については、SrcSrv tools と共にインストールされるサンプル Srcsrv.ini ファイルを参照してください。

### <a name="span-idusingadifferentlocationorfilenamespanspan-idusingadifferentlocationorfilenamespanusing-a-different-location-or-file-name"></a><span id="using_a_different_location_or_file_name"></span><span id="USING_A_DIFFERENT_LOCATION_OR_FILE_NAME"></span>別の場所またはファイル名を使用します。

既定では、SrcSrv は、ツールを Windows のデバッグのインストール ディレクトリの srcsrv サブディレクトリにある、Srcsrv.ini という名前のファイルをそのマスター構成ファイルとして使用します。

SRCSRV を設定して、別の構成ファイルを指定できます\_INI\_ファイル環境変数を目的のファイルの完全なパスとファイル名と同じです。

などの複数のユーザーが 1 つの構成ファイルを共有する場合、システムのすべてにアクセスできる共有に配置とし、次のような環境変数を設定、でした。

```console
set SRCSRV_INI_FILE=\\ourserver\ourshare\bestfile.txt
```

 

 





