# BaseAdapter
create baseadapter for your project



BaseAdapter.kt

abstract class BaseAdapter<in T : ViewDataBinding> : RecyclerView.Adapter<BaseViewHolder>() {

    override fun onCreateViewHolder(parent: ViewGroup, viewType: Int): BaseViewHolder = BaseViewHolder(
        DataBindingUtil.inflate(
            LayoutInflater.from(parent.context),viewType,parent,false))

    override fun getItemViewType(position: Int): Int {
        return getLayoutIdForPosition(position)
    }

    abstract fun getAnyForPosition(position: Int):Any
    //abstract fun getViewModel():T
    abstract fun getLayoutIdForPosition(position: Int):Int

}


BaseViewHolder.kt


class BaseViewHolder(viewDataBinding: ViewDataBinding) : RecyclerView.ViewHolder(viewDataBinding.root) {

    private val binding: ViewDataBinding?
    init {
        this.binding=viewDataBinding
    }


    fun bind(any: Any): ViewDataBinding?{
        binding?.setVariable(BR.any,any)
        //binding?.setVariable(BR.viewModel,viewModel)
        binding?.executePendingBindings()
        return binding
    }
}
