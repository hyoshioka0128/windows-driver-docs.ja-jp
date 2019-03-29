---
title: DMRC の WMIS サーバーの検索タイミングの判断方法
description: DMRC の WMIS サーバーの検索タイミングの判断方法
ms.assetid: dc68045e-85c2-443d-9e4d-099bbd21590d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3c80c21f3267cd4d88bada6f24df18260c276b51
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579346"
---
# <a name="how-the-dmrc-determines-when-to-search-the-wmis-server"></a>DMRC の WMIS サーバーの検索タイミングの判断方法


デバイス メタデータの取得のクライアント ([DMRC](device-metadata-retrieval-client.md)) デバイス メタデータ パッケージのキャッシュを保持します。 このキャッシュは、DMRC が Windows メタデータとインターネット サービスからダウンロードしたメタデータ パッケージが格納されます ([WMIS](windows-metadata-and-internet-services.md)) サーバー。

ときに、DMRC が UI に表示されるすべてのデバイスの最も適切なと現在のメタデータ パッケージのキャッシュを検索して、デバイスとプリンターまたは Device Stage ユーザー インターフェイス (Ui) を開いて、します。

定期的に、そのキャッシュからメタデータ パッケージを選択、前に、DMRC 検索を行うため、デバイスの新しいメタデータ パッケージ、 [WMIS](windows-metadata-and-internet-services.md)サーバー。 見つかった場合、DMRC、パッケージをダウンロードし、そのコンピューター上のキャッシュにインストールします。 次に、DMRC では、そのキャッシュからメタデータ パッケージの新しいバージョンを選択します。

次の値に基づいて、DMRC 決定を検索するときに、 [WMIS](windows-metadata-and-internet-services.md)デバイスの新しいメタデータ パッケージのサーバー。

<a href="" id="lastcheckeddate"></a>**LastCheckedDate**  
この値が最も、DMRC がデバイスのメタデータの WMIS サーバーを照会するときに最新の日付を示します。 この日付は、DMRC がメタデータ パッケージを正常にダウンロードするかどうかを反映しません。

それぞれのデバイス メタデータ パッケージのプロパティを含むインデックス テーブルを管理する、DMRC[デバイス ID](device-ids.md)システムで。 **LastCheckedDate**値が、このインデックス テーブルの各行のフィールド。

<a href="" id="checkbackmdnotretrieved"></a>**CheckBackMDNotRetrieved**  
このレジストリ値は、日数を示します、DMRC が待機する前に、デバイス メタデータ パッケージの WMIS サーバーのクエリを繰り返すことです。 この値は、対象の DMRC はまだダウンロードされてメタデータ WMIS からデバイスに適用されます。

**CheckBackMDNotRetrieved**値は、次のレジストリ キーの下にあります。

```cpp
HKLM\Software\Microsoft\Windows\CurrentVersion\Device Metadata
```

次の表の形式と値の範囲、 **CheckBackMDNotRetrieved**値。

| データ型  | 値の範囲         | 既定値 |
|------------|---------------------|---------------|
| [REG_DWORD](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types) | 0 ~ 256 の範囲 | 5             |

 

<a href="" id="checkbackmdretrieved"></a>**CheckBackMDRetrieved**  
このレジストリ値が日数を示すデバイス メタデータ パッケージを更新するためのクエリを実行する前に、DMRC を待機します。 この値は、デバイスを DMRC 以前にダウンロードしたメタデータ パッケージに適用されます。

**CheckBackMDRetrieved**値は、次のレジストリ キーの下にあります。

```cpp
HKLM\Software\Microsoft\Windows\CurrentVersion\Device Metadata
```

次の表の形式と値の範囲、 **CheckBackMDRetrieved**値。

| データ型  | 値の範囲         | 既定値 |
|------------|---------------------|---------------|
| [REG_DWORD](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types) | 0 ~ 256 の範囲 | 8             |

 

**注**  、WMIS サーバー、DMRC の協力の値を設定、 **CheckBackMDRetrieved**と**CheckBackMDNotRetrieved**クライアント上のレジストリ値システム。 これらの値は、ネットワークの状態に基づいて設定され、負荷分散します。 WMIS サーバーからの各応答は、クライアントの構成データを含み、DMRC 動作を制御します。

 

DMRC では、デバイスの新しいメタデータ パッケージの WMIS サーバーを検索する必要があるかどうかを判断する次の手順に従います。

1.  場合、ターゲット デバイスの[デバイス ID](device-ids.md)が表示されていない、DMRC インデックス テーブルには、デバイスのメタデータ パッケージの DMRC を検索、最初にします。 ここで、DMRC WMIS サーバーを照会します。

2.  場合、ターゲット デバイスの[デバイス ID](device-ids.md)が表示されているかどうかは、デバイス メタデータ パッケージ用にもう一度 WMIS サーバー クエリを実行する時間を DMRC、DMRC インデックス テーブルに計算します。 この場合は、次のように WMIS サーバーに照会、DMRC:

    1.  DMRC がの値を比較して、DMRC がデバイスのデバイス メタデータ パッケージをダウンロードした場合、 **CheckBackMDRetrieved** -今日の日付の値をレジストリ キー、 **LastCheckedDate**値。 場合、 **CheckBackMDRetrieved**値が小さい、DMRC WMIS サーバー クエリを実行します。

    2.  DMRC がの値を比較して、DMRC がデバイスのデバイス メタデータ パッケージが以前ダウンロードしない場合、 **CheckBackMDNotRetrieved** -今日の日付の値をレジストリ キー、 **LastCheckedDate**値。 場合、 **CheckBackMDNotRetrieved**値が小さい、DMRC WMIS サーバー クエリを実行します。

 

 





