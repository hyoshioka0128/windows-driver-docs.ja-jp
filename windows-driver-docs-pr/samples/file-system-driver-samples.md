---
title: ファイル システム ドライバーのサンプル
description: このディレクトリにドライバーのサンプルでは、デバイスのカスタムのファイル システム ドライバーを記述するための開始点を提供します。
ms.assetid: 9F2F995E-EA20-4877-B96C-5FF082CE886D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f4d87404dc5060cccff8358170a664a500375abc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550024"
---
# <a name="file-system-driver-samples"></a>ファイル システム ドライバーのサンプル


このディレクトリにドライバーのサンプルでは、デバイスのカスタムのファイル システム ドライバーを記述するための開始点を提供します。

## <a name="file-systems"></a>ファイル システム


| サンプル名      | ソリューション                                                           | 説明                                                                                                                                                                                                                                                                            |
|------------------|--------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| CDFS を含む             | [cdfs を含む](https://go.microsoft.com/fwlink/p/?LinkId=617642)            | CD-ROM のファイル システム (cdfs) ドライバーのサンプルは、リムーバブル メディアのファイル システム ドライバーです。                                                                                                                                                                                               |
| FastFAT          | [fastfat](https://go.microsoft.com/fwlink/p/?LinkId=620305)         | ファイル システム ドライバーでは、FastFAT ファイル システムの新しいファイル システムのモデルとして使用される Windows の受信トレイに基づいています。                                                                                                                                                                              |
| AVScan           | [avscan](https://go.microsoft.com/fwlink/p/?LinkId=617644)          | このフィルターは、ファイル内のデータを検査するファイルのトランザクションに対応したスキャナーです。 ウイルス対策は、この方法で動作可能性があります。                                                                                                                                                                 |
| CancelSafe       | [cancelSafe](https://go.microsoft.com/fwlink/p/?LinkId=617645)      | ミニフィルターがキャンセルの安全なキューの使用方法を示します。                                                                                                                                                                                                                              |
| CDO              | [cdo](https://go.microsoft.com/fwlink/p/?LinkId=617646)             | ミニフィルターと制御デバイス オブジェクト (CDO) を使用する例です。                                                                                                                                                                                                                   |
| [Change]           | [change](https://go.microsoft.com/fwlink/p/?LinkId=617647)          | リアルタイムでファイル変更を監視するトランザクションに対応したフィルターです。                                                                                                                                                                                                                    |
| Ctx              | [ctx](https://go.microsoft.com/fwlink/p/?LinkId=617648)             | インスタンス、ファイル、ストリーム、および、ミニフィルターのストリームのハンドルにコンテキストをアタッチする方法を示します。                                                                                                                                                                               |
| 削除           | [delete](https://go.microsoft.com/fwlink/p/?LinkId=617649)          | ファイルまたはストリームの削除を検出する方法を示します。                                                                                                                                                                                                                              |
| メタデータ マネージャー | [MetadataManager](https://go.microsoft.com/fwlink/p/?LinkId=617650) | ファイルをミニフィルターに対応するメタデータを格納するために使用する方法の例として機能します。 このサンプルの実装は、ファイルの変更がブロックする必要がありますまたは一時的にファイルを閉じる必要があります、ミニフィルターのシナリオを示しています。 |
| Minispy          | [minispy](https://go.microsoft.com/fwlink/p/?LinkId=617651)         | 監視し、システム内で発生した I/O、トランザクションのアクティビティ ログに記録するツール。                                                                                                                                                                                                  |
| NameChanger      | [NameChanger](https://go.microsoft.com/fwlink/p/?LinkId=617652)     | マッピングを使用して別の部分にボリュームの名前空間の 1 つの部分からディレクトリに移植します。 ミニフィルター、ディレクトリの列挙型へのエントリを挿入する、名前のプロバイダーとして機能することによってこの錯覚を維持して、転送先のディレクトリ変更通知                             |
| NullFilter       | [nullFilter](https://go.microsoft.com/fwlink/p/?LinkId=617653)      | フィルター マネージャーへの登録を単に示すミニフィルターします。                                                                                                                                                                                                            |
| パススルー      | [passThrough](https://go.microsoft.com/fwlink/p/?LinkId=617654)     | さまざまな種類の I/O 要求のコールバック関数を指定する方法を示します。                                                                                                                                                                                                    |
| スキャナー          | [scanner](https://go.microsoft.com/fwlink/p/?LinkId=617655)         | ファイル データのスキャナー例。 通常、ウイルス対策フィルターはこの型です。                                                                                                                                                                                                           |
| SimRep           | [simrep](https://go.microsoft.com/fwlink/p/?LinkId=617656)          | ファイル システム フィルターが開いているファイルを代替パスにリダイレクトする再解析ポイントの動作のようなファイル システムをシミュレートする方法について説明します。                                                                                                                                               |
| SwapBuffer       | [swapBuffers](https://go.microsoft.com/fwlink/p/?LinkId=617657)     | バッファー間でデータの読み取りや書き込みを切り替える方法を示します。 この手法は、暗号化のフィルターに特に便利です。                                                                                                                                                     |

 

 

 




