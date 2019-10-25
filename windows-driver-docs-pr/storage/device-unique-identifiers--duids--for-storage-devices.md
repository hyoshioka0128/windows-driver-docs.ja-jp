---
title: ストレージ デバイスのストレージ一意識別子 (DUID)
description: ストレージ デバイスのストレージ一意識別子 (DUID)
ms.assetid: 3846961c-5b75-4a1b-bced-601fc25bf071
keywords:
- ストレージドライバー WDK、DUIDs
- DUIDs WDK storage
- デバイスの一意の Id (WDK ストレージ)
- デバイス Id WDK ストレージ
- WDK 記憶域の識別子
- シリアル番号 WDK ストレージ
- デバイスレイアウト署名 WDK ストレージ
- 署名 WDK、storage
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 632cfd4e6c28c945b36b5d301ca8ff2b55a04af1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845177"
---
# <a name="device-unique-identifiers-duids-for-storage-devices"></a>ストレージ デバイスのストレージ一意識別子 (DUID)


ファイルシステムのアーキテクチャが複雑になり、オペレーティングシステムコンポーネントの数が増加し、イニシエーターがさまざまなハードウェアおよびソフトウェアパスを通じて記憶域ターゲットにアクセスするため、記憶装置を特定する手法が不十分になります。

たとえば、プラグアンドプレイ (PnP) マネージャーは、コンピューターの各デバイスの[インスタンス識別子 (id)](https://docs.microsoft.com/windows-hardware/drivers/install/instance-ids)を生成します。 各インスタンス ID は、デバイス[ツリー](https://docs.microsoft.com/windows-hardware/drivers/kernel/device-tree)内の1つのデバイスノードに対応し、デバイスが同じ場所にある場合は、デバイスを一意に識別します。 コンピューターを再起動すると、インスタンス Id は保持されますが、デバイスを別のバスや別のコンピューターに移動しても、同じままになりません。 その結果、記憶域ネットワーク (San) 内のアプリケーションや、分散ストレージを使用する環境で動作する Windows Vista 診断サービスなどの新しいシステムコンポーネントには、インスタンス Id が不十分です。 ハードディスクドライブが SMART failure を予測すると、診断サービスのイベントが生成されます。 このイベントには、ディスクが存在する可能性のあるすべてのコンピューターのハードディスクの障害を一意に識別する識別子と、接続可能なすべてのバス上の識別子が含まれている必要があります。 このため、インスタンス Id とその他の[デバイス識別文字列](https://docs.microsoft.com/windows-hardware/drivers/install/device-identification-strings)は不十分です。

Microsoft Cluster Service (MSCS) や Partition Manager などの一部のアプリケーションとシステムサービスでは、デバイスレイアウト署名 ([**storage\_device\_layout\_signature**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storduid/ns-storduid-_storage_device_layout_signature)) を使用して、でストレージデバイスを一意に識別します。クラスター. ただし、特定の状況下では、デバイスレイアウト署名はこの目的には不十分であり、次の制限があります。

-   署名が変更されるか、クリアされる可能性があります。

-   デバイスがスピンしていない場合、または署名が存在するセクターへのアクセスに問題がある場合は、署名を使用できない可能性があります。

-   ディスクが別のクラスターノードによって予約されている場合、署名は使用できません。 Mscs は、MSCS が実行されているノードに関連付けられているディスクのドライブレイアウトのみを読み取ることができます。 異なるクラスターノードのディスクにアクセスする必要があるソフトウェアでは、ディスクレイアウト署名の代わりにを使用する必要があります。

-   ドライブレイアウトの署名は、論理ユニット番号 (LUN) とそのスナップショットを区別するのに役立ちません。 LUN とそのスナップショットのコンテンツは同じであるため、ドライブレイアウト署名は同じになります。

シリアル番号は、デバイスの場所に依存しない記憶装置を一意に識別する、信頼性の高い手法となることがあります。 シリアル番号は、多くの場合、デバイスの照会データの一部として使用できます。 イニシエーターは、 [**IOCTL\_ストレージ\_クエリ\_プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_query_property)要求を使用して照会データを照会できます。また、ポートドライバーは、[**ストレージ\_デバイス\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ns-ntddstor-_storage_device_descriptor)構造にクエリの結果を報告します。 ただし、この方法では、問い合わせデータを報告しないデバイス (テープドライブなど) を識別することはできません。

### <a name="span-iddevice_unique_identifiers__duids_spanspan-iddevice_unique_identifiers__duids_spandevice-unique-identifiers-duids"></a><span id="device_unique_identifiers__duids_"></span><span id="DEVICE_UNIQUE_IDENTIFIERS__DUIDS_"></span>デバイスの一意識別子 (DUIDs)

多くの場合、デバイスを一意に識別する手法はテクノロジの進化に伴って古くなっているため、Microsoft ではデバイスの一意 ID (DUID) と呼ばれるデバイス ID 形式を開発しています。これは拡張可能で、デバイスを識別するための新しい手法を組み込むことができます。使用できるようになります。

DUID は、[**ストレージ\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storduid/ns-storduid-_storage_device_unique_identifier)によって定義され、一意の\_識別子構造\_ます。この構造の最初のバージョン (DUID\_version\_1) には、次の識別子の組み合わせが含まれています。

<span id="STORAGE_DEVICE_ID_DESCRIPTOR"></span><span id="storage_device_id_descriptor"></span>[**ストレージ\_デバイス\_ID\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ns-ntddstor-_storage_device_id_descriptor)  
ストレージ\_デバイスの\_ID\_記述子の構造には、デバイスの重要製品データ (VPD) の0x83 ページから抽出された識別子が含まれています。 通常、このページをサポートしているのは SCSI およびファイバーチャネルデバイスのみです。 統合ドライブエレクトロニクス (IDE) デバイスとユニバーサルシリアルバス (USB) デバイス、IEEE 1394 ドライブ、および RAID コントローラーでは、0x83 ページは提供されません。

<span id="STORAGE_DEVICE_DESCRIPTOR"></span><span id="storage_device_descriptor"></span>[**ストレージ\_デバイス\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ns-ntddstor-_storage_device_descriptor)  
ストレージ\_デバイス\_記述子の構造体には、 **SerialNumberOffset**メンバーの単位シリアル番号へのオフセットなど、他の照会データが含まれています。 シリアル番号は、可変長の**NULL**で終わる文字列として書式設定されます。 記憶装置が SCSI に準拠している場合、ポートドライバーは、VPD のオプションのユニットシリアル番号ページ (ページ 0x80) からシリアル番号を抽出しようとします。 記憶装置が IDE デバイスの場合、ポートドライバーはデバイスの識別データからシリアル番号を生成します。

<span id="STORAGE_DEVICE_LAYOUT_SIGNATURE"></span><span id="storage_device_layout_signature"></span>[**ストレージ\_デバイス\_レイアウト\_署名**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storduid/ns-storduid-_storage_device_layout_signature)  
ストレージ\_デバイス\_レイアウト\_署名には、デバイスレイアウト署名が含まれています。

今後のバージョンでは、より多くのデータが DUIDs に追加されます。

DUIDs は固定サイズではないため、DUIDs (DUID コンシューマーと呼ばれます) を使用するソフトウェアは、ストレージ\_デバイス\_一意の\_識別子構造の**サイズ**メンバーから DUID のサイズを取得する必要があります。 DUID のバージョンは、この同じ構造体の、使用可能な * * * のメンバーで利用できます。

一部のデバイスでは、デバイスの DUID がすべての使用とすべての DUID コンシューマーに対して十分に一意であることを保証するために十分な情報を提供していません。 オペレーティングシステムがデバイスの VPD から一意の Id を取得できる場合は、すべての DUID コンシューマーに対して十分に一意な DUID を作成できます。 ただし、システムでデバイスレイアウト署名だけから DUID を作成する必要がある場合、duid は、一部の DUID コンシューマーに対しては十分に一意になりますが、他のコンシューマーには十分にはありません。

システムは、次の特性を持つ DUID を作成しようとします。

-   オペレーティングシステムを再起動しても、DUID は変わりません。

-   デバイスがあるコンピューターから別のコンピューターまたは別のアダプターに移動した場合や、チャネルが別のチャネルに移動された場合でも、DUID は同じままです。

-   DUID は、メディアではなく、デバイスを識別します。 この区別は、リムーバブルメディアを持つドライブにとって重要です。

-   マルチパスシステムでは、DUID はすべての i/o パスで同じになります。

DUIDs には次の制限があります。

-   多くの場合、DUIDs には、表示できないバイナリコンテンツが含まれています。

-   DUIDs は、常に**null**で終わるとは限りません。 DUID コンシューマーは、[**ストレージ\_デバイス\_レイアウト\_署名**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storduid/ns-storduid-_storage_device_layout_signature)構造の**サイズ**メンバーをチェックして、duid の長さを確認する必要があります。

-   DUID コンシューマーは、バイト単位で比較するのではなく、 [**Comparestorageduids**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storduid/nf-storduid-comparestorageduids)を使用して duids を比較する必要があります。

-   *列挙子*は、プラグアンドプレイ (PnP) のためにデバイスオブジェクトを識別するために duids を使用しないようにする必要があります。 マルチパスシステムには、同じ DUID を共有する複数のデバイスを含めることができます。 ただし、PnP の場合、デバイス Id は一意である必要があります。

イニシエーターは、 [**IOCTL\_ストレージ\_クエリ\_プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_query_property)ID が**StorageDeviceUniqueIdProperty**である、プロパティ ID を使用して、DUID 情報データを照会できます。

### <a name="span-idhow_to_compare_duidsspanspan-idhow_to_compare_duidsspanhow-to-compare-duids"></a><span id="how_to_compare_duids"></span><span id="HOW_TO_COMPARE_DUIDS"></span>DUIDs を比較する方法

DUID コンシューマーは、2つの Duid を比較するために、Storduids .h で定義されている[**Comparestorageduids**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storduid/nf-storduid-comparestorageduids)ルーチンを使用する必要があります。 **Comparestorageduids**は、2つの duids が一致するかどうかを示す[**DUID\_\_STATUS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storduid/ne-storduid-_duid_match_status)値に一致する DUID を返します。 操作が成功した場合、 **Comparestorageduids**は次のいずれかの値を返します。

<span id="DuidExactMatch"></span><span id="duidexactmatch"></span><span id="DUIDEXACTMATCH"></span>**DuidExactMatch**  
2つの DUIDs のすべてのフィールドが正確に一致します。

<span id="DuidSubIdMatch"></span><span id="duidsubidmatch"></span><span id="DUIDSUBIDMATCH"></span>**DuidSubIdMatch**  
DUID は複数のサブ Id で構成されています。 少なくとも1つのサブ Id が一致し、2つの DUIDs が同じデバイスを表していると想定されます。 デバイスのファームウェアが更新されると、新しい識別子が取得される可能性があります。これにより、デバイスの DUID の構成が変更されます。 DUID コンシューマーがデバイスの古い DUID を新しい DUID と比較した場合、 [**Comparestorageduids**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storduid/nf-storduid-comparestorageduids)は**DuidExactMatch**の代わりに**duidsubidmatch**を返すことがあります。 これは、サブ ID に基づく有効な一致の例です。 DUID コンシューマーは、DUID コンシューマーの要件に応じて、 **Duidsubidmatch**戻り値を一致として受け入れるか、不一致として受け入れるかを選択する必要があります。

<span id="DuidNoMatch"></span><span id="duidnomatch"></span><span id="DUIDNOMATCH"></span>**DuidNoMatch**  
シリアル番号が一致しません。また、重要な製品データ (VPD) のページ83h から一意のサブ Id が一致していません。

前の値に加えて、 [**Comparestorageduids**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storduid/nf-storduid-comparestorageduids)はさまざまなエラーコードを返す場合があります。

[**Comparestorageduids**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storduid/nf-storduid-comparestorageduids)ルーチンは、次のアルゴリズムを使用して2つの duid を比較します。

1.  完全一致があるかどうかを確認します。 DUIDs 内のすべてのデータが一致する場合、DUIDs は正確に一致し、 [**Comparestorageduids**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storduid/nf-storduid-comparestorageduids)は**DuidExactMatch**を返します。 それ以外の場合は、次のチェックを続行します。

2.  VPD 識別子を確認します。 一意のサブ Id が一致する場合、DUIDs match と[**Comparestorageduids**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storduid/nf-storduid-comparestorageduids)は**Duidsubidmatch**を返します。 サブ Id が一致しない場合、またはデバイスが一意の VPD 識別子を提供しない場合は、次のチェックを続行します。

3.  ユニットのシリアル番号を確認します。 ベンダー ID、製品 ID、およびシリアル番号が同じである場合、DUIDs match と[**Comparestorageduids**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storduid/nf-storduid-comparestorageduids)は**Duidsubidmatch**を返します。 これらの値のいずれも一致しない場合、またはデバイスがこれらの値を提供しない場合は、次のチェックを続行します。

4.  ドライブレイアウトの署名を確認します。 2つの DUIDs のドライブレイアウト署名が一致する場合、DUIDs match と[**Comparestorageduids**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storduid/nf-storduid-comparestorageduids)は**Duidsubidmatch**を返します。 ドライブの署名が一致しない場合、またはシステムがデバイスのドライブレイアウト署名を読み取ることができない場合、DUIDs は一致せず、 **Comparestorageduids**は**duidnomatch**を返します。

 

 




