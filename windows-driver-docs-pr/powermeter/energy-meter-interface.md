---
title: エネルギー メーター インターフェイス
description: エネルギー メーター インターフェイス
keywords:
- エネルギー使用状況の測定と予算の WDK インターフェイスします。
- エネルギー メーター インターフェイス WDK
- PMI WDK エネルギー メーター
ms.date: 11/17/2017
ms.localizationpriority: medium
ms.openlocfilehash: a1edcf28b1894f685cf20d23f93a77941a791a99
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354928"
---
# <a name="energy-meter-interface"></a>エネルギー メーター インターフェイス

Windows 10 以降、ドライバーはクライアントにエネルギー消費量データを公開するエネルギー使用状況測定インターフェイス (EMI) を実装できます。 このインターフェイスは、一連の標準化された Ioctl エネルギー データと使用状況測定のハードウェアおよび従量制課金されているハードウェアに関するデータを取得するクライアントで構成されます。 

オンボード エネルギー メーターが定期的に電圧とレールの上の現在の測定、電源の製品を計算して時間の経過と共に使用された総エネルギーの統合します。 これらの計算方法は、既存のものから個別[電力メーター インターフェイス](https://docs.microsoft.com/windows-hardware/drivers/powermeter/power-meter-interface)概念電力メーターがグローバルの平均間隔。 エネルギー メーターでは、現在までのエネルギー総消費量を返すことによって、ニーズに応じてさまざまな間隔で平均電力を判断する複数のコンシューマーを使用できます。  

EMI インターフェイスは、目的のクライアント アプリケーションとサービスが消費するエネルギー データのコンジットを提供します。  クライアントは、最新の値から前の値を減算して、前回のクエリ以降に使用された電力を計算し、必要に応じて、単純な除算して平均電力に変換します。 

## <a name="discovering-devices-that-implement-emi"></a>EMI を実装するデバイスの検出

クライアントの呼び出しを通じて EMI をサポートするデバイスを検出する[SetupDiEnumDeviceInterfaces](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdienumdeviceinterfaces)と[SetupDiGetDeviceInterfaceDetail](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceinterfacedetaila)します。 メータリング EMI 準拠は、システムに存在するデバイスごとのエネルギーの EMI デバイス インターフェイスの 1 つのインスタンスが作成されます。 

EMI デバイス インターフェイスの GUID は **{45BD8344-7ED6-49cf-A440-C276C933B053}** emi.h で定義されている、します。 コードは、この GUID を指定するのに GUID_DEVICE_ENERGY_METER を別の方法として使用できます。 

## <a name="using-the-emi-interface"></a>EMI インターフェイスを使用します。

クライアント コードは、通常、次のプロセスを使用する EMI とやり取りします。

1. 呼び出す[IOCTL_EMI_GET_VERSION](https://docs.microsoft.com/windows/desktop/api/emi/ni-emi-ioctl_emi_get_version) EMI インターフェイスのバージョンが、返されるデバイスでサポートされていることを確認および[EMI_VERSION](https://docs.microsoft.com/windows/desktop/api/emi/ns-emi-emi_version)値。 Windows 10 では、デバイスは EMI_VERSION_V1 をサポートできます。 Windows 10 バージョン 1809、デバイスが EMI_VERSION_V2 もサポートできます。 オペレーティング システムの今後のリリースでは、以降のバージョンを生じる可能性があります。 

2. EMI メタデータのサイズを取得する IOCTL_EMI_GET_METADATA_SIZE を呼び出します。 

3. 必要な呼び出しと EMI メタデータのサイズのバッファーを割り当てる[IOCTL_EMI_GET_METADATA](https://docs.microsoft.com/windows/desktop/api/emi/ni-emi-ioctl_emi_get_metadata)します。 返される EMI_MEASUREMENT_UNIT が EmiMeasurementUnitPicowattHours であることを確認します。 Windows 10 の後のリリースでは、追加のユニットの種類を定義できます。 

4. エネルギー総消費量を測定するには、呼び出す[IOCTL_EMI_GET_MEASUREMENT](https://docs.microsoft.com/windows/desktop/api/emi/ni-emi-ioctl_emi_get_measurement)します。 返される AbsoluteEnergy 値[EMI_CHANNEL_MEASUREMENT_DATA 構造](https://docs.microsoft.com/windows/desktop/api/emi/ns-emi-emi_channel_measurement_data)picowatt 時間外の任意の 0 ポイントとの合計累積エネルギーは、します。 一般に、2 つの異なる時刻でサンプルを比較し、その間隔のエネルギー消費量のエネルギーの値を減算する必要があります。 

5. 平均電力消費量を測定するには、呼び出す[IOCTL_EMI_GET_MEASUREMENT](https://docs.microsoft.com/windows/desktop/api/emi/ni-emi-ioctl_emi_get_measurement)先頭と必要な間隔の終了。 AbsoluteEnergy と AbsoluteTime 値を減算、 [EMI_CHANNEL_MEASUREMENT_DATA 構造](https://docs.microsoft.com/windows/desktop/api/emi/ns-emi-emi_channel_measurement_data)から以前のサンプルの後者のサンプルで返されます。

詳細については、これらのトピックを参照してください。

[EMI Ioctl](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/dn957425(v=vs.85)) -エネルギー測定インターフェイス (EMI) ではサポートされている I/O 制御コード (Ioctl) について説明します。
 
[EMI 列挙型と構造体](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/dn957424(v=vs.85))-このセクションでは、列挙型およびエネルギー測定インターフェイス (EMI) によってサポートされる構造について説明します。
 


 




