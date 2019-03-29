---
title: 移植に関する問題のチェックリスト
description: 移植に関する問題のチェックリスト
ms.assetid: 6ab26321-85b8-4a5b-8ca5-af6cbf56ccd6
keywords:
- 64 ビットの WDK カーネル、ドライバーの移植
- 64 ビット Windows に移植ドライバー
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: ab2d63a59ae3a3fdfe5f81e3dc3d73a87b6a36d5
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349795"
---
# <a name="porting-issues-checklist"></a>移植に関する問題のチェックリスト





### <a name="general"></a>全般

-   新しい 64 ビット セーフ Windows のデータ型を使用します。

    このドキュメントの前半で説明されている、新しい 64 ビット セーフ データ型は、Basetsd.h で定義されます。 このヘッダー ファイルには、Ntdef.h Ntddk.h、Wdm.h、および Ntifs.h に含まれているが含まれます。

-   プラットフォームのコンパイラ マクロを慎重に使用します。

    次の前提は無効になりました。

    ```cpp
    #ifdef _WIN32  // 32-bit Windows code
    ...
    #else          // 16-bit Windows code
    ...
    #endif
    ```

    ただし、64 ビット コンパイラは、定義\_旧バージョンとの互換性のための WIN32 します。

    また、次の前提は無効になりました。

    ```cpp
    #ifdef _WIN16  // 16-bit Windows code
    ...
    #else          // 32-bit Windows code
    ...
    #endif
    ```

    この場合、else 句を表すことができます\_WIN32 または\_WIN64 します。

-   適切な形式指定子を使用して、 **printf**と**wsprintf**します。

    使用 **%p**を 16 進数でポインターを印刷します。 これは、印刷のポインターの最適な選択肢です。

    **注**  サポートは今後のバージョンの Visual C **%I**ポリモーフィックなデータを印刷します。 これは、64 ビット Windows で 32 ビットに 32 ビット Windows の 64 ビットの値を扱います。 Visual C もサポート **%i64** 64 ビット値を出力します。

     

<!-- -->

-   アドレス空間を確認します。

    無条件と見なさないでください、たとえば、アドレスがカーネル アドレスの場合、上位ビット必要があります設定することです。 システムの最も低いアドレスを取得する、 **MM\_LOWEST\_システム\_アドレス**マクロ。

### <a name="pointer-arithmetic"></a>ポインターの算術演算

-   符号なしと符号付きの操作を実行するときに注意します。

    次の点を考慮します。

    ```cpp
    ULONG x;
    LONG y;
    LONG *pVar1;
    LONG *pVar2;
     
    pVar2 = pVar1 + y * (x - 1);
    ```

    問題が発生するため、 *x*が式全体が署名されていないため、署名なし、します。 これがうまく機能しない限り、 *y*が負の値。 この場合、 *y*変換は、スケールとに追加された 32 ビットの有効桁数を使用して、式を評価する符号なしの値*pVar1*します。 64 ビットの Windows でこの 32 ビット符号なしの負の値数は大規模な 64 ビット正の数が正しくない結果になります。 この問題を解決するには宣言*x*符号付きの値として、または明示的に型キャストに**長い**式で。

-   16 進数の定数と符号なしの値を使用する場合は注意します。

    次のアサーションは、64 ビット システムではありません。

    ```cpp
    ~((UINT64)(PAGE_SIZE-1)) == (UINT64)~(PAGE_SIZE-1)
    PAGE_SIZE = 0x1000UL  // Unsigned long - 32 bits
    PAGE_SIZE - 1 = 0x00000fff
    ```

    LHS 式:

    ```cpp
    // Unsigned expansion(UINT64)(PAGE_SIZE -1 ) = 0x0000000000000fff
    ~((UINT64)(PAGE_SIZE -1 )) = 0xfffffffffffff000
    ```

    RHS 式:

    ```cpp
    ~(PAGE_SIZE-1) = 0xfffff000
    (UINT64)(~(PAGE_SIZE - 1)) = 0x00000000fffff000
    ```

    そのため。

    ```cpp
    ~((UINT64)(PAGE_SIZE-1)) != (UINT64)(~(PAGE_SIZE-1))
    ```

-   操作ではなく気を付けます。

    次の点を考慮します。

    ```cpp
    UINT_PTR a; ULONG b;
    a = a & ~(b - 1); 
    ```

    問題は、その ~(b−1) 生成 0x0000 0000 *xxxx xxxx*と 0 xffff いない FFFF *xxxx xxxx*します。 コンパイラでは、この検出はありません。 これを解決するには、次のように、コードを変更します。

    ```cpp
    a = a & ~((UINT_PTR)b - 1);
    ```

-   バッファー サイズを計算するときに注意します。

    次の点を考慮します。

    ```cpp
    len = ptr2 - ptr1 
    /* len could be greater than 2**32 */
    ```

    ポインターをキャスト**PCHAR**ポインターの算術演算の。

    **注**  場合*len*が宣言されている**INT**または**ULONG**、これはコンパイラの警告が生成されます。 バッファー サイズ、正しく計算する場合でもがまだの容量を超える**ULONG**します。

     

-   計算またはハード コーディングされたポインターのオフセットを使用しないでください。

    構造体を使用する場合は、使用、 [**フィールド\_オフセット**](https://msdn.microsoft.com/library/windows/hardware/ff545727)マクロ限り構造体メンバーのオフセットを決定します。

-   ハード コーディングされたポインターまたはハンドル値を使用しないでください。

    ハード コーディングされたポインターまたはハンドル (ハンドル) 0 xffffffff などに渡さないルーチンなど**ZwCreateSection**します。 代わりに、無効ななどの定数を使用して、\_処理\_値は、各プラットフォームの適切な値が設定するために定義できます。

-   64 ビットの Windows で 0 xffffffff は、いない-1 と同じです。

    例:

    ```cpp
    DWORD index = 0;
    CHAR *p;

    // if (p[index-1] == '0') causes access violation on 64-bit Windows!
    ```

    32 ビット コンピューター。

    ```cpp
    p[index-1] == p[0xffffffff] == p[-1] 
    ```

    64 ビット コンピューター。

    ```cpp
    p[index-1] == p[0x00000000ffffffff] != p[-1]
    ```

    この問題を回避するにはの型の変更を*インデックス*から**DWORD**に**DWORD\_PTR**します。

### <a name="polymorphism"></a>ポリモーフィズム

- ポリモーフィックなインターフェイスを持つように注意します。

  型のパラメーターを受け取る関数を作成しない**DWORD** (またはその他の固定精度の型) のポリモーフィックなデータ。 パラメーターの型にする必要があります、データは、ポインターまたは整数値には場合、 **UINT\_PTR**または**PVOID**ではなく、 **DWORD**します。

  たとえば、として型指定された例外パラメーターの配列を受け取る関数を作成しない**DWORD**値。 配列の配列を指定する必要があります**DWORD\_PTR**値。 そのため、配列の要素には、アドレスまたは 32 ビット整数値を保持できます。 元の型がある場合、一般的な規則は**DWORD**ポインターの幅に変換する必要があると、 **DWORD\_PTR**値。 対応するネイティブの Win32 型のポインターの有効桁数の型があるためにです。 使用するコードがあれば**DWORD**、 **ULONG**、またはポリモーフィックな方法では、その他の 32 ビット型 (つまり、本当にするアドレスを保持するために、パラメーターまたは構造体のメンバー) を使用して、 **UINT\_PTR**現在の型の代わりにします。

- ポインターを OUT パラメーター関数を呼び出す際に注意します。

  これを行わない。

  ```cpp
  void GetBufferAddress(OUT PULONG *ptr);
  {
    *ptr=0x1000100010001000;
  }
  void foo()
  {
    ULONG bufAddress;
    //
    // This call causes memory corruption.
    //
    GetBufferAddress((PULONG *)&bufAddress);
  }
  ```

  型キャスト*bufAddress*に (**PULONG** \*)、コンパイラ エラーを防止します。 ただし、 *GetBufferAddress*メモリ位置に、64 ビット値を書き込む *& bufAddress*します。 *BufAddress*のみ 32 ビット値の直後、32 ビットは、 *bufAddress*は上書きされます。 これは、非常に微妙な見つかりにくいバグです。

- ポインターをキャストできません**INT**、**長い**、 **ULONG**、または**DWORD**します。

  いくつかのビットをテストするへのポインターをキャストする必要があります場合、セットまたはビットをオフにまたはそれ以外の場合、コンテンツの操作を使用して、 **UINT**\_**PTR**または**INT** \_**PTR**型。 これらの型は整数型の Windows の 32 ビットと 64 ビットの両方のポインターのサイズに拡張すること (たとえば、 **ULONG** 32 ビット Windows 用と **\_int64** 64 ビット Windows 用)。 たとえば、次のコードを移植するとします。

  ```cpp
  ImageBase = (PVOID)((ULONG)ImageBase | 1);
  ```

  移植プロセスの一環としては、次のようにコードを変更するは。

  ```cpp
  ImageBase = (PVOID)((ULONG_PTR)ImageBase | 1);
  ```

  使用**UINT**\_**PTR**と**INT**\_**PTR**適切な場所 (とされるかどうかがない場合必要に応じて、ありませんケースだけで使用しても問題)。 ポインター型にキャストしません**ULONG**、**長い**、 **INT**、 **UINT**、または**DWORD**します。

  **注****処理**として定義されます、 **void \\** <em>ので型キャスト、**処理</em>* に値**ULONG**値をテスト、設定、または安値をオフにする 2 つのビットは、プログラミング エラーです。  

     

- 使用**PtrToLong**と**PtrToUlong**ポインターを切り捨てます。

  場合は、32 ビット値へのポインターを切り捨てる必要がありますを使用して、 **PtrToLong**または**PtrToUlong**関数 (で定義されている*Basetsd.h*)。 この関数は、呼び出しの間のポインター切り捨ての警告を無効にします。

  これらの関数を慎重に使用します。 結果のキャストしないポインター変数がこれらの関数のいずれかを使用して、切り捨て後**長い**または**ULONG**ポインターに戻す。 これらの関数は、最初に参照したポインターがメモリにアクセスする必要は通常、アドレスの上位 32 ビットを切り捨てます。 慎重に検討することがなくこれらの関数を使用して、脆弱なコードが発生します。

### <a name="data-structures-and-structure-alignment"></a>データ構造体と構造体の配置

-   データ構造体のポインターのすべての使用を慎重に確認するには。

    次に、一般的な問題の領域を示します。

    -   ディスクに格納されているまたは 32 ビット プロセスで交換されるデータ構造体。
    -   明示的および暗黙的な共用体のポインター。
    -   セキュリティ記述子。

<!-- -->

-   使用して、 [**フィールド\_オフセット**](https://msdn.microsoft.com/library/windows/hardware/ff545727)マクロ。

    以下に例を示します。

    ```cpp
    struct xx {
       DWORD NumberOfPointers;
       PVOID Pointers[1];
    };
     
    ```

    次の割り当ては、コンパイラが 8 バイト アラインメントの要件をさらに 4 バイトの構造体に埋め込まれますので、64 ビット Windows で適切です。

    ```cpp
    malloc(sizeof(DWORD)+100*sizeof(PVOID)); 
     
    ```

    それを正しく行う方法を次に示します。

    ```cpp
    malloc(FIELD_OFFSET(struct xx, Pointers) +100*sizeof(PVOID));
    ```

-   使用して、**型\_配置**マクロ。

    **型\_配置**マクロは、現在のプラットフォームで特定のデータ型のアラインメント要件を返します。 以下に例を示します。

    ```cpp
    TYPE_ALIGNMENT(KFLOATING_SAVE) == 4 on x86, 8 on Itanium
    TYPE_ALIGNMENT(UCHAR) == 1 everywhere
    ```

    たとえば、このようなコード。

    ```cpp
    ProbeForRead(UserBuffer, UserBufferLength, sizeof(ULONG));
    ```

    移植性に変更されたときのようになります。

    ```cpp
    ProbeForRead(UserBuffer, UserBufferLength, TYPE_ALIGNMENT(ULONG));
    ```

-   カーネルのパブリック構造体のデータ型の変更を監視します。

    たとえば、**情報**フィールドに、IO\_状態\_ブロック構造は、現在型の**ULONG\_PTR**します。

-   構造体のパッキング ディレクティブを使用する場合は注意してください。

    64 ビットの Windows の場合は、データ構造がずれている場合は、ルーチン操作する構造体など[ **RtlCopyMemory** ](https://msdn.microsoft.com/library/windows/hardware/ff561808)と**memcpy**、エラーは発生しません。 代わりに、例外が発生します。 例:

    ```cpp
    #pragma pack (1)  /* also set by /Zp switch */
    struct Buffer {
        ULONG size;
        void *ptr;
    };

    void SetPointer(void *p) {
        struct Buffer s;
        s.ptr = p;  /* will cause alignment fault */
        ...
    }
    ```

    使用できます、**整列されていない**マクロでこの問題を解決します。

    ```cpp
    void SetPointer(void *p) {
        struct Buffer s;
        *(UNALIGNED void *)&s.ptr = p;
    }
    ```

    残念ながらを使用して、**整列されていない**マクロは Itanium ベースのプロセッサで非常に不経済です。 構造体の先頭に、64 ビットの値とポインターを格納することをお勧めします。

    **注**  可能であれば、同じヘッダー ファイルで異なるパッキング レベルの使用を回避します。

     

### <a name="additional-information"></a>追加情報

-   [64 ビット ドライバーでの 32 ビットの I/O のサポート](supporting-32-bit-i-o-in-your-64-bit-driver.md)

-   [準備の 64 ビット Windows](https://msdn.microsoft.com/library/windows/desktop/aa384198) (ユーザー モード アプリケーションの移植ガイド)

 

 




