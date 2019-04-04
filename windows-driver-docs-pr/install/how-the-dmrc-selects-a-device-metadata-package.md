---
title: DMRC のデバイス メタデータ パッケージの選択方法
description: DMRC のデバイス メタデータ パッケージの選択方法
ms.assetid: dbedc995-520a-4b54-8613-d5a7810ab99c
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 48545d2f50c2cf8f11ca0fd2ea601707f28b5b9f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579726"
---
# <a name="how-the-dmrc-selects-a-device-metadata-package"></a>DMRC のデバイス メタデータ パッケージの選択方法


ときに、デバイスとプリンターまたは Device Stage ユーザー インターフェイスが開かれ、オペレーティング システムの起動時、デバイス メタデータの取得のクライアント ([DMRC](device-metadata-retrieval-client.md)) デバイスの最も適切なと現在のメタデータ パッケージのキャッシュを検索します。 Windows メタデータとインターネット サービスにデバイスの新しいメタデータ パッケージの DMRC が検索されます ([WMIS](windows-metadata-and-internet-services.md)) サーバー。 見つかった場合、DMRC、パッケージをダウンロードし、コンピューターにインストールします。

**注**  DMRC が最近のデバイス メタデータ パッケージをダウンロードする場合、新しいパッケージの WMIS server 検索ではなく、デバイスのキャッシュされたメタデータ パッケージを使用します。 詳細については、[、DMRC が WMIS サーバーを検索するタイミングを決定する方法](how-the-dmrc-determines-when-to-search-the-wmis-server.md)を参照してください。

 

DMRC は、パッケージで指定された、次のメタデータ XML 要素を使用して、デバイスの適切なパッケージを選択します。 これらの XML 要素の順序では、DMRC はメタデータ パッケージの選択を使用して、優先順位が反映されます。

-   [**ModelID** ](https://msdn.microsoft.com/library/windows/hardware/ff549295)と[ **ModelIDList**](https://msdn.microsoft.com/library/windows/hardware/ff549303)

-   [**HardwareID** ](https://msdn.microsoft.com/library/windows/hardware/ff546114)と[ **HardwareIDList**](https://msdn.microsoft.com/library/windows/hardware/ff546121)

-   [**ロケール**](https://msdn.microsoft.com/library/windows/hardware/ff548647)

-   [**LastModifiedDate**](https://msdn.microsoft.com/library/windows/hardware/ff548624)

[DMRC](device-metadata-retrieval-client.md)デバイス メタデータ パッケージを選択するとこれらの手順に従います。

1.  デバイスは、モデル ID を持つ場合、DMRC が間の一致をデバイス メタデータ パッケージを検索、 [ **ModelID** ](https://msdn.microsoft.com/library/windows/hardware/ff549295)パッケージのエントリ[ **ModelIDList** ](https://msdn.microsoft.com/library/windows/hardware/ff549303)XML 要素と、デバイスのモデル ID の値。

2.  間で一致、DMRC がデバイス メタデータ パッケージを検索、デバイスが、モデル ID を持たない場合、 [ **HardwareID** ](https://msdn.microsoft.com/library/windows/hardware/ff546114)パッケージのエントリ[ **HardwareIDList**](https://msdn.microsoft.com/library/windows/hardware/ff546121) XML 要素と、デバイスのハードウェア Id。

3.  DMRC はデバイスの一覧に対して、手順 1. および 2. で説明されている検索条件を満たすメタデータ パッケージを作成します。 この一覧から、DMRC し、一覧のエントリの一致を検索、パッケージの間で[**ロケール**](https://msdn.microsoft.com/library/windows/hardware/ff548647) XML 要素との一覧は、コンピューターのユーザー ロケールを優先します。

    この検索条件に一致するリスト内のエントリがない場合、DMRC を持つロケール XML 要素を含むデバイス メタデータ パッケージのリストにエントリを検索、**既定**属性に設定**true**します。 DMRC 一致が見つかった場合は、そのメタデータ パッケージを選択します。

4.  含むパッケージ、DMRC には、手順 3 では、複数のデバイス メタデータ パッケージが検出されると、選択、 [ **LastModifiedDate** ](https://msdn.microsoft.com/library/windows/hardware/ff548624)を最新のタイムスタンプを持つ XML 要素。

次の点がによって使用される選択アルゴリズムに関連する、 [DMRC](device-metadata-retrieval-client.md):

-   DMRC では、ハードウェア Id に基づいているメタデータ パッケージを選択する場合は、オペレーティング システムのドライバーのインストール中に使用するハードウェア Id のランク付けと同じが使用されます。 DMRC には、以下に固有のハードウェア Id よりも大きいより固有のハードウェア Id が順位付けされます。 たとえば、次のハードウェア Id はランク順に一覧表示します。

    ```cpp
    <HardwareID>DOID:USB\VID_XXXX&PID_YYYY&REV_0000</HardwareID>
    <HardwareID>DOID:USB\VID_XXXX&PID_YYYY</HardwareID>
    ```

    ハードウェア Id については、[ハードウェア Id](hardware-ids.md)を参照してください。

-   デバイス メタデータ パッケージを 1 つだけを設定する必要があります、**既定**の属性、 [**ロケール**](https://msdn.microsoft.com/library/windows/hardware/ff548647) XML 要素を**true**します。 この属性は、順位付け値が最も高いハードウェア ID を含むパッケージで true にのみ設定する必要があります。

-   [ **LastModifiedDate** ](https://msdn.microsoft.com/library/windows/hardware/ff548624) XML 要素はバージョン管理の目的で使用し、デバイスのデバイス メタデータ パッケージの新しいバージョンを選択するために使用します。

-   ローカルのメタデータ ストアに 2 つ以上のデバイス メタデータ パッケージに同じ値が含まれている場合、 [ **ModelIDList**](https://msdn.microsoft.com/library/windows/hardware/ff549303)、 [ **HardwareIDList** ](https://msdn.microsoft.com/library/windows/hardware/ff546121)、 [**ロケール**](https://msdn.microsoft.com/library/windows/hardware/ff548647)、または[ **LastModifiedDate** ](https://msdn.microsoft.com/library/windows/hardware/ff548624) DMRC の XML 要素では、デバイスのうち 1 つのみが選択されます。 この場合、DMRC 選択これらのパッケージのいずれかの非決定的な方法でします。

デバイス メタデータの XML スキーマと要素の詳細については、[デバイス メタデータのスキーマ リファレンス](https://msdn.microsoft.com/library/windows/hardware/ff541452)を参照してください。

 

 





