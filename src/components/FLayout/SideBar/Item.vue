<script>
export default {
  name: 'Item',
  functional: true,
  props: {
    icon: {
      type: String,
      default: ''
    },
    title: {
      type: String,
      default: ''
    },
    imgUrl: {
      type: String,
      default: ''
    }
  },
  render(h, context) {
    const { icon, title } = context.props
    const vnodes = []
    if (icon) {
      if (icon.includes('el-icon')) {
        vnodes.push(<i class={[icon, 'sub-el-icon']}/>)// icon为elementui的官方组件
      } else if (icon.includes('icon-')) {
        vnodes.push(<i class={['iconfont', icon, 'sub-el-icon']} />) // iconfont字体
      } else {
        vnodes.push(<img class='sub-el-icon' src={icon} />) // 图片
      }
    }

    if (title) {
      vnodes.push(<span slot='title'>{(title)}</span>)
    }
    console.log('vnodes :>> ', vnodes);
    return vnodes
  }
}
</script>

<style>
/* 根据全局样式设置icon颜色 */
.sub-el-icon{
  color: currentColor;
  width: 1rem;
  height: 1rem;
}
</style>