---
title: ファイル システム フィルター ドライバーのクラスおよびクラスの Guid
description: ファイル システム フィルター ドライバーのクラスおよびクラスの Guid
ms.assetid: dd247b06-4529-4818-9239-b89c25f5c1df
keywords:
- WDK の Guid はファイル システム
- クラス Guid の WDK ファイル システム
- WDK のクラスはファイル システム
- フィルター ドライバー WDK ファイル システム、クラス
- ファイル システム フィルター ドライバー WDK、クラス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6787d8b4cb6787cfae6003d263b42001a6e8d1ae
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530664"
---
# <a name="file-system-filter-driver-classes-and-class-guids"></a>ファイル システム フィルター ドライバーのクラスおよびクラスの Guid


## <span id="ddk_file_system_filter_driver_classes_and_class_guids_if"></span><span id="DDK_FILE_SYSTEM_FILTER_DRIVER_CLASSES_AND_CLASS_GUIDS_IF"></span>


Microsoft Windows XP およびそれ以降のオペレーティング システムは、ファイル システム フィルター ドライバーのセットアップ クラスを提供します。 これらのクラスは、ハードウェア デバイスのシステム提供のデバイス セットアップ クラスを提供する機能のサブセットを提供します。 (ハードウェア デバイスのセットアップ クラスの詳細については、次を参照してください[デバイス セットアップ クラス](https://msdn.microsoft.com/library/windows/hardware/ff541509)。)。

各セットアップ クラスは、クラスの GUID に関連付けられています。 システム定義のクラス Guid は devguid.h で定義されます。

このトピックでは、ファイル システム フィルター ドライバーのセットアップ クラスを使用します。 各クラスの定義で、**クラス**と**ClassGuid**エントリで指定する必要があります値を含める、 [ **INF バージョン セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547502)のフィルターの INF ファイル。 フィルター ドライバーには、クラスとドライバーの INF ファイルで指定されているロード順序グループに一致する GUID を使用する必要があります。

デバイスの場合、またはに加え、INF ファイル内の適切なクラス GUID 値を指定して、**クラス** = *クラス名*エントリのパフォーマンスを大幅に向上します。システム INF ファイルを検索します。

次の一覧には、システム定義のクラスおよびファイル システム フィルター ドライバーのクラスの Guid が含まれています。 このリストのエントリは、Windows XP 以降のオペレーティング システムでファイル システム フィルター ドライバーに対して作成されたロード順序グループに対応します。

**注**  セットアップ クラスとは見なされませんいて、したがってクラスに割り当てられた Guid がないため、ボックスの一覧で、次の 3 つのロード順序グループは表示されません。フィルター、FSFilter、上下 FSFilter します。

 

<span id="FSFilter_Activity_Monitor"></span><span id="fsfilter_activity_monitor"></span><span id="FSFILTER_ACTIVITY_MONITOR"></span>FSFilter 利用状況モニター<br/>
クラス ActivityMonitor を =<br/>
ClassGuid = {b86dff51-a31e-4bac-b3cf-e8cfe75c9fc2}

<span id="FSFilter_Undelete"></span><span id="fsfilter_undelete"></span><span id="FSFILTER_UNDELETE"></span>FSFilter 削除の取り消し<br/>
クラス = 削除の取り消し<br/>
ClassGuid = {fe8f1572-c67a-48c0-bbac-0b5c6d66cafb}

<span id="FSFilter_Anti-Virus"></span><span id="fsfilter_anti-virus"></span><span id="FSFILTER_ANTI-VIRUS"></span>FSFilter ウイルス対策<br/>
クラスのウイルス対策を =<br/>
ClassGuid = {b1d1a169-c54f-4379-81db-bee7d88d7454}

<span id="FSFilter_Replication"></span><span id="fsfilter_replication"></span><span id="FSFILTER_REPLICATION"></span>FSFilter レプリケーション<br/>
クラスのレプリケーションを =<br/>
ClassGuid = {48d3ebc4-4cf8-48ff-b869-9c68ad42eb9f}

<span id="FSFilter_Continuous_Backup"></span><span id="fsfilter_continuous_backup"></span><span id="FSFILTER_CONTINUOUS_BACKUP"></span>FSFilter 継続的なバックアップ<br/>
クラス ContinuousBackup を =<br/>
ClassGuid = {71aa14f8-6fad-4622-ad77-92bb9d7e6947}

<span id="FSFilter_Content_Screener"></span><span id="fsfilter_content_screener"></span><span id="FSFILTER_CONTENT_SCREENER"></span>FSFilter コンテンツこだわりの検索<br/>
クラス ContentScreener を =<br/>
ClassGuid = {3e3f0674-c83c-4558-bb26-9820e1eba5c5}

<span id="FSFilter_Quota_Management"></span><span id="fsfilter_quota_management"></span><span id="FSFILTER_QUOTA_MANAGEMENT"></span>FSFilter クォータの管理<br/>
クラス QuotaManagement を =<br/>
ClassGuid = {8503c911-a6c7-4919-8f79-5028f5866b0c}

<span id="FSFilter_Cluster_File_System"></span><span id="fsfilter_cluster_file_system"></span><span id="FSFILTER_CLUSTER_FILE_SYSTEM"></span>FSFilter クラスター ファイル システム<br/>
クラス CFSMetaDataServer を =<br/>
ClassGuid = {cdcf0939-b75b-4630-bf76-80f7ba655884}

<span id="FSFilter_HSM"></span><span id="fsfilter_hsm"></span><span id="FSFILTER_HSM"></span>FSFilter HSM<br/>
クラスの HSM を =<br/>
ClassGuid = {d546500a-2aeb-45f6-9482-f4b1799c3177}

<span id="FSFilter_Compression"></span><span id="fsfilter_compression"></span><span id="FSFILTER_COMPRESSION"></span>FSFilter 圧縮<br/>
クラスの圧縮を =<br/>
ClassGuid = {f3586baf-b5aa-49b5-8d6c-0569284c639f}

<span id="FSFilter_Encryption"></span><span id="fsfilter_encryption"></span><span id="FSFILTER_ENCRYPTION"></span>FSFilter 暗号化<br/>
クラスの暗号化を =<br/>
ClassGuid = {a0a701c0-a511-42ff-aa6c-06dc0395576f}

<span id="FSFilter_Physical_Quota_Management"></span><span id="fsfilter_physical_quota_management"></span><span id="FSFILTER_PHYSICAL_QUOTA_MANAGEMENT"></span>FSFilter 物理クォータの管理<br/>
クラス PhysicalQuotaManagement を =<br/>
ClassGuid = {6a0a8e78-bba6-4fc4-a709-1e33cd09d67e}

<span id="FSFilter_Open_File"></span><span id="fsfilter_open_file"></span><span id="FSFILTER_OPEN_FILE"></span>開いている FSFilter ファイル<br/>
クラス OpenFileBackup を =<br/>
ClassGuid = {f8ecafa6-66d1-41a5-899b-66585d7216b7}

<span id="FSFilter_Security_Enhancer"></span><span id="fsfilter_security_enhancer"></span><span id="FSFILTER_SECURITY_ENHANCER"></span>FSFilter セキュリティ強化<br/>
クラス SecurityEnhancer を =<br/>
ClassGuid = {d02bc3da-0c8e-4945-9bd5-f1883c226c8c}

<span id="FSFilter_Copy_Protection"></span><span id="fsfilter_copy_protection"></span><span id="FSFILTER_COPY_PROTECTION"></span>FSFilter コピー防止<br/>
クラス CopyProtection を =<br/>
ClassGuid = {89786ff1-9c12-402f-9c9e-17753c7f4375}

<span id="FSFilter_System"></span><span id="fsfilter_system"></span><span id="FSFILTER_SYSTEM"></span>FSFilter システム<br/>
クラス FSFilterSystem を =<br/>
ClassGuid = {5d1b9aaa-01e2-46af-849f-272b3f324c46}

<span id="FSFilter_Infrastructure"></span><span id="fsfilter_infrastructure"></span><span id="FSFILTER_INFRASTRUCTURE"></span>FSFilter インフラストラクチャ<br/>
クラスのインフラストラクチャを =<br/>
ClassGuid = {e55fa6f9-128c-4d04-abab-630c74b1453a}
 

 




