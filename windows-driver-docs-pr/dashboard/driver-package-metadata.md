---
title: ドライバー パッケージ メタデータ
description: パートナー センター申請のためのドライバー パッケージ メタデータの構造について説明します。
author: balapv
ms.author: balapv
ms.topic: article
ms.date: 08/21/2018
ms.openlocfilehash: e3f4022d4715fc8d76b3c749df74db56ba5cf4d1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56518736"
---
# <a name="driver-package-metadata"></a>ドライバー パッケージ メタデータ

ドライバー メタデータ パッケージは、申請に関連付けられているファイルです。 メタデータ パッケージには、ドライバー パッケージまたはバンドル内の各 INF ファイルに関する詳細が含まれています。 このファイルは、[Get a submission](get-a-submission.md) メソッドを使用してダウンロードすることができます。 そのファイルは、[リンク オブジェクト](get-product-data.md#link-object)の *rel* - **driverMetadata** で使用できます。 

## <a name="driver-metadata-structure"></a>ドライバー メタデータの構造

```json
{
  "BundleInfoMap": {
    "dc3b111e-c750-4a55-96ce-0eae1d1da8a2": {
      "Locales": [
        "English"
      ],
      "InfInfoMap": {
        "foo_bar.inf": {
          "DriverPackageFamilyId": "RAID-foo_bar.inf",
          "InfClass": "SCSIAdapter",
          "DriverVersion": "1.1.1.1",
          "DriverDate": "2018-01-11T00:00:00",
          "ExtensionId": null,
          "Provider": "RAID",
          "ClassGuid": "{a43418dc-cfc9-42e1-85b0-2d644331e214}",
          "InstallationComputerHardwareIds": [
            "a9a8e6fc-4969-4336-927c-9d8f7b6c1d14",
            "a4a127cb-2c10-464e-abb5-e78fcdf0d3c3"
          ],
          "OSPnPInfoMap": {
            "WINDOWS_v100_RS3_FULL": {
              "pci\\ven_test&dev_abcd": {
                "Manufacturer": "RAID",
                "DeviceDescription": "Virtual Raid Adapter",
                "FeatureScore": null
              }
            }
          }
        }
      }
    }
  }
}
```

ファイルに含まれる値は次のとおりです。

| Value | 種類 | 説明 |
|:--|:--|:--|
|BundleInfoMap|オブジェクト|これは親です。 GUID で示され、ドライバー バンドルに関するすべての詳細が含まれています。 この値は、[ハードウェア ID オブジェクト](get-shipping-labels.md#hardware-id-object)の *bundleID* にマップします|
|ロケール|文字列の配列|バンドルに該当するロケールの配列|
|InfInfoMap|オブジェクトの配列|バンドル内の各 INF ファイルを記述する配列。 各項目の識別子は、INF ファイル名です。 INF 名は、[ハードウェア ID オブジェクト](get-shipping-labels.md#hardware-id-object)の *infID* にマップします。|
|DriverPackageFamilyId|string|ドライバー パッケージ ファミリの ID|
|InfClass|string|ドライバーのデバイス クラスまたは INF クラス|
|DriverVersion|string|ドライバーのバージョン|
|DriverDate|datetime|このドライバーの日時|
|ExtensionId|GUID|拡張 INF に適用されます。 この INF の拡張機能 ID を表す GUID です|
|プロバイダー|string|このドライバーのプロバイダー|
|ClassGuid|string|ドライバーのクラス GUID|
|InstallationComputerHardwareIds|GUID の配列|このドライバーをターゲットにできる CHID のリスト|
|OSPnPInfoMap|オブジェクトの配列|オペレーティング システムをハードウェア ID にマップするオブジェクトの配列。 オブジェクトには基本要素があり、それはオペレーティング システムです。 各オペレーティング システムの内部は、PNP またはハードウェア ID とその詳細のリストです。 オペレーティング システムは[ハードウェア ID オブジェクト](get-shipping-labels.md#hardware-id-object)の operatingSystemCode にマップし、ハードウェア ID は *pnpString* にマップします|
|製造元|string|ハードウェア ID の製造元|
|DeviceDescription|string|ハードウェア ID の説明|
|FeatureScore|string|ドライバーの機能スコア|

## <a name="see-also"></a>関連項目

- [ハードウェア ダッシュボード API のサンプル (GitHub)](https://aka.ms/hpc_async_api_samples)
