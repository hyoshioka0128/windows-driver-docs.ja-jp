---
title: 記憶装置のデバイス一意識別子 (DUID)
description: 記憶装置のデバイス一意識別子 (DUID)
ms.assetid: 3846961c-5b75-4a1b-bced-601fc25bf071
keywords:
- ストレージ ドライバー WDK、Duid
- Duid WDK ストレージ
- デバイスの一意の Id の WDK ストレージ
- デバイス Id の WDK ストレージ
- 識別子の WDK ストレージ
- シリアル番号の WDK ストレージ
- デバイス レイアウト署名 WDK ストレージ
- WDK、記憶域の署名
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c9906f16975c3d3c5139c121da512c0a9560d1da
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365255"
---
# <a name="device-unique-identifiers-duids-for-storage-devices"></a>記憶装置のデバイス一意識別子 (DUID)


ファイル システムのアーキテクチャがより複雑になると、オペレーティング システムのコンポーネントの数を乗算し、およびイニシエーターがますます多様なハードウェアとソフトウェアのパスを通じてストレージ ターゲットをアクセスと、ストレージ デバイスを識別するための手法が不適切になります。

たとえば、プラグ アンド プレイ (PnP) マネージャーが生成されます、[インスタンス識別子 (ID)](https://msdn.microsoft.com/library/windows/hardware/ff547656)コンピューター内の各デバイス。 ID は、1 つのデバイス ノードに対応する各インスタンス、[デバイス ツリー](https://msdn.microsoft.com/library/windows/hardware/ff543194)デバイスが同じ場所に残っている場合、デバイスを一意に識別します。 コンピューターを再起動するがないは、同じデバイスを別のバスまたは別のコンピューターに移動する場合、インスタンス Id が保持されます。 その結果、インスタンス Id がストレージ エリア ネットワーク (San) 内のアプリケーションと一部の新しいシステム コンポーネント、Windows Vista の診断サービスなどの環境で分散ストレージで動作するための適切です。 ハード ディスク ドライブは、スマート障害を予測すると、診断のサービスのイベントが生成されます。 このイベントは、障害が発生したハード ディスク、ディスクにあるすべてのコンピューターとに関連付けることがすべてのバスを一意に識別する識別子を含める必要があります。 インスタンスの Id およびその他の[識別文字列](https://msdn.microsoft.com/library/windows/hardware/ff541224)はこの目的に適していません。

一部のアプリケーションおよび Microsoft Cluster Service (MSCS) と、パーティション マネージャーなどのシステム サービスを使用して、デバイスのレイアウトのシグネチャ ([**ストレージ\_デバイス\_レイアウト\_署名** ](https://msdn.microsoft.com/library/windows/hardware/ff566973)) クラスターで記憶域デバイスを一意に識別します。 ただし、デバイス レイアウトの署名がこの目的は、特定の状況下で十分でないと、次の制限が含まれています。

-   署名は変わる可能性があります。 またはクリアします。

-   デバイスが回転していないか、署名が存在する場所、セクターへのアクセスの問題がある場合に、署名を利用できない可能性があります。

-   署名が、ディスクが別のクラスター ノードによって予約されている場合に使用できます。 MSCS では、MSCS がで実行されているノードに関連付けられているディスクのみのドライブのレイアウトを読み取ることができます。 別のクラスター ノードでディスクにアクセスする必要があるソフトウェアには、代わりに、ディスク レイアウトの署名を使用する必要があります。

-   ドライブのレイアウトの署名は、論理ユニット番号 (LUN) とそのスナップショットを区別することはできません。 LUN とそのスナップショットは、まったく同じ内容であるために、そのドライブのレイアウトのシグネチャは同じになります。

シリアル番号は、デバイスの場所に依存しないストレージ デバイスを一意に識別する信頼性の高い方法でがあります。 シリアル番号は、多くの場合、デバイスの照会のデータの一部として使用できます。 イニシエーターを照会でデータを照会できます、 [ **IOCTL\_ストレージ\_クエリ\_プロパティ**](https://msdn.microsoft.com/library/windows/hardware/ff560590)レポートでクエリの結果の要求、およびポート ドライバー、[**ストレージ\_デバイス\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff566971)構造体。 ただし、この手法では、照会データを報告しないいるテープ ドライブなどのデバイスの識別は役立ちません。

### <a name="span-iddeviceuniqueidentifiersduidsspanspan-iddeviceuniqueidentifiersduidsspandevice-unique-identifiers-duids"></a><span id="device_unique_identifiers__duids_"></span><span id="DEVICE_UNIQUE_IDENTIFIERS__DUIDS_"></span>デバイスの一意の識別子 (Duid)

Microsoft がデバイス一意の ID (DUID) は拡張可能にして、そのデバイスを識別するための新しい技法を組み込むことができますと呼ばれるデバイス ID の形式を開発したため、多くの場合、デバイスを一意に識別するための手法は不要になるテクノロジの進化に伴って、有効になります。

によって、DUID が定義されている、 [**ストレージ\_デバイス\_UNIQUE\_識別子**](https://msdn.microsoft.com/library/windows/hardware/ff566975)構造、およびこの構造体の最初のバージョン (DUID\_バージョン\_1) は次の識別子の組み合わせが含まれています。

<span id="STORAGE_DEVICE_ID_DESCRIPTOR"></span><span id="storage_device_id_descriptor"></span>[**記憶域\_デバイス\_ID\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff566972)  
記憶域\_デバイス\_ID\_記述子構造体には、デバイスの重要製品データ (VPD) のページ 0x83 から抽出された識別子が含まれています。 通常、SCSI、ファイバー チャネル デバイスだけでは、このページをサポートします。 統合されたドライブ electronics (IDE) とユニバーサル シリアル バス (USB) デバイス、IEEE 1394 ドライブ、ページ 0x83 RAID コント ローラーを指定しないとします。

<span id="STORAGE_DEVICE_DESCRIPTOR"></span><span id="storage_device_descriptor"></span>[**記憶域\_デバイス\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff566971)  
記憶域\_デバイス\_記述子構造体には、単体のシリアル番号にオフセットを含むその他の照会データが含まれています、 **SerialNumberOffset**メンバー。 シリアル番号が可変長として書式設定された**NULL**-で終わる文字列。 記憶域デバイスは、SCSI に準拠していませんが、ポート、ドライバーは、VPD の省略可能なユニットのシリアル番号ページ (ページ 0x80) からのシリアル番号を抽出しようとします。 ポート ドライバーがからシリアル番号を生成する記憶装置が IDE デバイスの場合は、デバイスのデータを識別します。

<span id="STORAGE_DEVICE_LAYOUT_SIGNATURE"></span><span id="storage_device_layout_signature"></span>[**記憶域\_デバイス\_レイアウト\_署名**](https://msdn.microsoft.com/library/windows/hardware/ff566973)  
記憶域\_デバイス\_レイアウト\_署名にはデバイス レイアウトのシグネチャが含まれています。

多くのデータに適用されます Duid 将来のバージョン。

Duid (DUID コンシューマーと呼ばれます) の使用を行うソフトウェアから DUID のサイズを取得する必要がありますように Duid は、固定サイズではありません、**サイズ**記憶域のメンバー\_デバイス\_UNIQUE\_識別子構造体。 DUID のバージョンは、バージョンで使用可能な * * * これと同じ構造のイオン メンバー。

一部のデバイスでは、システム、デバイスの DUID はすべての使用とすべての DUID 利用者にとって十分であることを保証するための十分な情報は提供されません。 場合は、オペレーティング システムでは、デバイスの VPD から一意の Id を取得できます、DUID のすべてのコンシューマーに対して十分に一意である DUID を作成することができます。 DUID を十分に一意になりますシステムする必要がありますから作成する場合、DUID デバイス レイアウト署名だけで、他のユーザーではなく一部 DUID コンシューマー。

システムは、次の特性を持つ DUID を作成しようとします。

-   DUID では、オペレーティング システムを再起動すると、同じままです。

-   DUID は別に、デバイスが別のコンピューターに、別の 1 つのアダプターまたは 1 つのチャネルから移動したときにも、同じです。

-   デバイスとメディアではなく、DUID を識別します。 この違いは、リムーバブル メディアのドライブに重要です。

-   マルチパスのシステムでは、DUID は、すべての I/O パスのと同じです。

Duid には、次の制限があります。

-   Duid には、バイナリ コンテンツ表示できないには多くの場合が含まれます。

-   Duid、必ずしも**null**-終了します。 DUID コンシューマーを確認する必要があります、**サイズ**のメンバー、 [**ストレージ\_デバイス\_レイアウト\_署名**](https://msdn.microsoft.com/library/windows/hardware/ff566973)構造体をDUID の長さを決定します。

-   DUID コンシューマーを使用する必要があります[ **CompareStorageDuids** ](https://msdn.microsoft.com/library/windows/hardware/ff552464)と比較する 1 バイトずつではなく Duid を比較します。

-   *列挙子*Duid をプラグ アンド プレイ (PnP) のためのデバイス オブジェクトを識別するために使用しないでください。 マルチパスのシステムには、同じ DUID を共有するデバイスを 1 つ以上のことができます。 ただし、PnP デバイス Id 一意でなければなりません。

イニシエーターが DUID 情報データを使用するために照会できます、 [ **IOCTL\_ストレージ\_クエリ\_プロパティ**](https://msdn.microsoft.com/library/windows/hardware/ff560590)のプロパティ ID で要求**StorageDeviceUniqueIdProperty**します。

### <a name="span-idhowtocompareduidsspanspan-idhowtocompareduidsspanhow-to-compare-duids"></a><span id="how_to_compare_duids"></span><span id="HOW_TO_COMPARE_DUIDS"></span>Duid を比較する方法

DUID コンシューマーを使用する必要があります、 [ **CompareStorageDuids** ](https://msdn.microsoft.com/library/windows/hardware/ff552464)ルーチンは、2 つの Duid を比較する、Storduids.h で定義されています。 **CompareStorageDuids**を返します、 [ **DUID\_一致\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff552760) 2 つの Duid と一致しているかどうかを示す値です。 操作が成功すると、 **CompareStorageDuids**値は次のいずれかを返します。

<span id="DuidExactMatch"></span><span id="duidexactmatch"></span><span id="DUIDEXACTMATCH"></span>**DuidExactMatch**  
2 つの Duid のすべてのフィールドを正確に一致します。

<span id="DuidSubIdMatch"></span><span id="duidsubidmatch"></span><span id="DUIDSUBIDMATCH"></span>**DuidSubIdMatch**  
DUID はいくつかのサブ Id で構成をされます。 少なくとも 1 つのサブ Id が一致すると、および 2 つの Duid が同じデバイスを表す可能性があります。 デバイスのファームウェアが更新されたときに、新しい識別子は、デバイスの DUID の構成を変更を取得、可能性があります。 場合は DUID コンシューマー デバイスの新しい DUID での古い DUID を比較する[ **CompareStorageDuids** ](https://msdn.microsoft.com/library/windows/hardware/ff552464)返す可能性があります**DuidSubIdMatch**の代わりに**DuidExactMatch**します。 これは、サブ ID に基づいて有効な一致の例です。 DUID コンシューマーが受け付けることがあるかどうかを選択する必要があります、 **DuidSubIdMatch**一致または DUID コンシューマーの要件に応じて、不一致として値を取得します。

<span id="DuidNoMatch"></span><span id="duidnomatch"></span><span id="DUIDNOMATCH"></span>**DuidNoMatch**  
シリアル番号が一致しないと、一致する 83 h 重要製品データ (VPD) のページからサブ一意の Id がないです。

前述の値だけでなく[ **CompareStorageDuids** ](https://msdn.microsoft.com/library/windows/hardware/ff552464)さまざまなエラー コードを返す可能性があります。

[ **CompareStorageDuids** ](https://msdn.microsoft.com/library/windows/hardware/ff552464)ルーチンでは、次のアルゴリズムを使用して、2 つの Duid を比較します。

1.  完全一致を確認します。 場合はすべて、Duid 内のデータの一致、Duid 一致と[ **CompareStorageDuids** ](https://msdn.microsoft.com/library/windows/hardware/ff552464)返します**DuidExactMatch**します。 それ以外の場合は、次のチェックに進みます。

2.  VPD 識別子を確認します。 一意のサブ Id が一致、Duid 一致する場合と[ **CompareStorageDuids** ](https://msdn.microsoft.com/library/windows/hardware/ff552464)返します**DuidSubIdMatch**します。 サブ Id が一致しない、またはデバイスが VPD 一意識別子を提供していないは、次のチェックを続行します。

3.  ユニットのシリアル番号を確認します。 ベンダー ID、製品 ID、およびシリアル番号が同じ場合、Duid が一致と[ **CompareStorageDuids** ](https://msdn.microsoft.com/library/windows/hardware/ff552464)返します**DuidSubIdMatch**します。 一致するこれらの値がない、またはデバイスがこれらの値を指定していないは、次のチェックを続行します。

4.  ドライブのレイアウトの署名を確認します。 2 つの Duid のドライブ レイアウトの署名が一致、Duid 一致する場合と[**CompareStorageDuids** ](https://msdn.microsoft.com/library/windows/hardware/ff552464)返します**DuidSubIdMatch**します。 Duid が一致しない場合は、ドライブの署名が一致しないか、システムは、デバイスのドライブのレイアウトの署名を読み取ることができません、および**CompareStorageDuids**返します**DuidNoMatch**します。

 

 




