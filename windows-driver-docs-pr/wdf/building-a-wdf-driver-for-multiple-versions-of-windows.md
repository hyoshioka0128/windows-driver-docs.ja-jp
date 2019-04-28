---
title: Windows の複数バージョン用 WDF ドライバーのビルド
description: 説明する複数のバージョンの Windows 用のドライバーを WDF をビルドする方法。
ms.date: 04/06/2018
ms.localizationpriority: medium
ms.openlocfilehash: 85816ea4d802853f730b5279e83724d4f4890b3f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376922"
---
# <a name="building-a-wdf-driver-for-multiple-versions-of-windows"></a>Windows の複数バージョン用 WDF ドライバーのビルド

WDF は常に許可すると、1 回、ドライバーを作成し、Windows の複数のバージョンで、生成されたバイナリを使用していますが、Windows 10 バージョン 1803 (Redstone 4)、前にこの"以前ビルドで実行する新しい"に制限されていました WDF 追加 Windows 10 バージョン 1803 以降、「ビルド新しい、古いで実行」の条件付きの実行の追加特典を使用します。 要約。
* **既存の**:新しいバージョンのメジャー バージョンを提供するフレームワークが含まれる Windows のバージョンで実行する framework の旧バージョンでビルドされたバイナリと一致します。 たとえば、KMDF 1.9 (Windows 7) で構築されたドライバーは、Windows 8 システム (KMDF 1.11) で実行されます。 例では、ドライバーは、KMDF 1.9 の機能に制限されます。
* **追加**:KMDF 版 1.25 および UMDF バージョン 2.25 on Windows 10 バージョン 1803 以降、framework の新しいバージョンのドライバーをビルドして、バイナリの結果として得られるドライバーが (最低限の Windows 10 バージョン 1803) で Windows の以前のバージョンで実行されます。 さらに、ドライバーは、のみが新しいフレームワークのバージョンで利用できる機能を条件付きで使用できます。

つまりことだけでなくは、ドライバーでは実行、Windows の将来のバージョンが常に、Windows 10 バージョン 1803 に過去のバージョンでは、実行もします。

これを行う 2 つの手順がある: Visual Studio でのビルド設定を指定して、API の呼び出しまたは構造体または存在することができない可能性がありますまたは可能性のあるフィールドにアクセスする前にランタイム チェックを実行します。

**注意**:この機能は省略可能ですし、ドライバーでのみ有効に WDF の最新機能を持たない Windows の以前のバージョンで読み込み可能なまま WDF の最新機能を使用するドライバーをビルドする必要があります。

設定しない場合**マイナー バージョン (ターゲットのバージョン)** または**マイナー バージョン (最低限必要です)**、バージョン管理が以前と同じままです。

## <a name="specifying-minimum-required"></a>最低限必要なを指定します。

Visual Studio で新しい構成設定は次のとおりです。
* **KMDF バージョンのマイナー (最低限必要です)**
* **UMDF バージョンのマイナー (最低限必要です)**

この変更に従って、既存の 2 つの設定の名前が更新されました。
* **KMDF バージョン マイナー** -> **KMDF バージョンのマイナー (ターゲットのバージョン)**
* **UMDF バージョン マイナー** -> **UMDF バージョンのマイナー (ターゲットのバージョン)**

設定しない場合**最低限必要な**、Visual Studio ビルドを**ターゲット バージョン**up、およびダウンレベルのサポートは提供されません。 これは、以前の動作と一致**マイナー バージョン**プロパティ。

設定する場合**最低限必要な**、次の要件が適用されます。
* 25 < = 最低限必要です < ターゲット バージョンを =
* **構成プロパティには、ドライバーが]-> [設定]、[全般] を [** に設定して、`_NT_TARGET_VERSION`に`0x0A000005`(RS4) またはそれ以降。

## <a name="checking-if-functionality-is-present"></a>チェック機能が存在するかどうか

API、構造体、または存在することができない可能性がありますまたは可能性のあるメンバーの使用はすべて、前に、WdfFuncEnum.h で定義されている次のマクロのいずれかを呼び出す必要があります。

```cpp
BOOLEAN
WDF_IS_FUNCTION_AVAILABLE (
    FunctionName
    );

BOOLEAN
WDF_IS_STRUCTURE_AVAILABLE (
    StructName
    );

BOOLEAN
WDF_IS_FIELD_AVAILABLE (
    StructName,
    FieldName
    );
```

次の例を検討してください。  WDF v29 がリリースされると、新しい API を追加します。**WdfSomeNewFeature**します。 設定した場合**ターゲット バージョン**29 と**最低限必要な**を 25 に修正の結果として得られるドライバーが読み込まれる、29 を 25 からのすべての framework バージョンで (および beyond、メジャー バージョンを変更しない限り) 呼び出しバージョン 25Api は、前などし、v29 API の各呼び出しの前に次のチェックは。

```cpp
if (WDF_IS_FUNCTION_AVAILABLE(WdfSomeNewFeature)) {
    WdfSomeNewFeature();
}
```

条件付きチェックを行わない場合、次の操作を表示可能性があります。
-   NTSTATUS が返される API 呼び出しはエラー コードを返します。
-   場合は、API には、NTSTATUS 以外のものが返されます。
    - KMDF:マシンのバグを確認します。
    - UMDF:DriverStop エラー WudfHost プロセスがクラッシュします。
-   ドライバーの検証が有効になっている場合も、ドライバーがクラッシュします。 これは、テスト環境で問題を識別するのに役立ちます。
-   サイレント メモリの破損 (構造体またはフィールドへのアクセス) する場合。

ドライバー クラッシュには、障害が発生したドライバー名、フレームワーク名、および失敗した API のインデックスが含まれています。 API の名前を取得するには、WDFFUNCENUM WdfFuncEnum.h 内の値を検索します。

WDF の Visual Studio のプロパティの詳細については、次を参照してください。[ドライバー プロジェクトのモデルの設定のプロパティをドライバー](../develop/driver-model-settings-properties-for-driver-projects.md)します。
