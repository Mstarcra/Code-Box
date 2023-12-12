search 搜尋

PHP的部分，中間其實還有else if 是分頁相關的我先省略比較易讀
```

if (isset($_GET["search-coupon"])) {
    $search = $_GET["search-coupon"];
    // echo $search;

    $sql = "SELECT * FROM coupon    
    WHERE name LIKE '%$search%' OR discount LIKE '%$search%' OR requirement LIKE '%$search%' AND valid=1  ORDER BY id ASC";
}else {
    $page=1;
    $order=1;
    $sql = "SELECT * FROM coupon WHERE valid=1 ORDER BY id ASC LIMIT 0,$perPage";
}

$result = $conn->query($sql);
$rows = $result->fetch_all(MYSQLI_ASSOC);
```
HTML的部分
```
<div class="py-1">
    <form action="">
        <div class="row g-3 align-items-center">

            <?PHP if (isset($_GET["search-coupon"])) : ?>
                <div class="col-auto">
                    <a class="btn btn-dark" href="coupons-list.php">
                        <i class="bi bi-backspace"></i>
                    </a>

                </div>
            <?PHP endif; ?>

            <div class="col-auto">
                <input type="text" class="form-control text-start " name="search-coupon" value="<?PHP $searchCoupon = isset($_GET["search-coupon"]) ? $search : "";
                                                                                                echo $searchCoupon; ?>" placeholder="可以搜尋名稱、折扣金額" required>
            </div>

            <div class="col-auto">
                <button class="btn btn-dark text-white" type="submit">
                    <i class="fa-solid fa-magnifying-glass"></i>
                </button>
            </div>
        </div>
    </form>
</div>
```

如果跟你們的升降序或分頁功能打架的話可能就要HTML再斟酌加入條件
```
<?PHP if (!isset($_GET["search-coupon"])) : ?>
  升降序或分頁功能
<?PHP endif; ?>
```
