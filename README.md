# -
利用ConvenientBanner去实现
首先添加依赖
compile 'com.bigkoo:convenientbanner:2.0.5'


然后布局
<com.bigkoo.convenientbanner.ConvenientBanner
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:id="@+id/convenientBanner"
    android:layout_width="match_parent"
    android:layout_height="200dp"
    app:canLoop="true" //一直循环
/>

写逻辑代码 翻页
mConvenientBanner.setPages(new CBViewHolderCreator<NetworkImageHolderView>() {
        @Override
        public NetworkImageHolderView createHolder() {
      //返回图片
            return new NetworkImageHolderView();
        }
    }, 


//mJsonBeen.get(0).getImgUrl(),mJsonBeen.get(1).getImgUrl(),mJsonBeen.get(2).getImgUrl())是网址  
//setPageIndicator(new int[]{R.mipmap.ic_page_indicator,R.mipmap.ic_page_indicator_focused})小圆点
//setPageIndicatorAlign(ConvenientBanner.PageIndicatorAlign.CENTER_HORIZONTAL);小圆点显示的位置

Arrays.asList(mJsonBeen.get(0).getImgUrl(),mJsonBeen.get(1).getImgUrl(),mJsonBeen.get(2).getImgUrl())).setPageIndicator(new int[]{R.mipmap.ic_page_indicator,R.mipmap.ic_page_indicator_focused}).setPageIndicatorAlign(ConvenientBanner.PageIndicatorAlign.CENTER_HORIZONTAL);


写NetworkImageHolderView类

public class NetworkImageHolderView implements Holder<String> {
    private ImageView imageView;

    @Override
    public View createView(Context context) {
        imageView = new ImageView(context);
        imageView.setScaleType(ImageView.ScaleType.CENTER_CROP);
        return imageView;
    }
    @Override
    public void UpdateUI(Context context, int position, String data) {
        Glide.with(context).load(data).into(imageView);
    }
}

