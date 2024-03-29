import java.util.ArrayList;
import java.util.Scanner;
import java.io.File;
import java.io.IOException;
import java.util.Arrays;

public class AirlineProblem {

    public static void main(String[] args){
        Scanner scannerToReadAirlines = null;
        try{
            scannerToReadAirlines = new Scanner(new File("airlines.txt"));
       
       }
        catch(IOException e){
            System.exit(0);
        }
        if(scannerToReadAirlines != null){
            ArrayList<Airline> airlinesPartnersNetwork = new ArrayList<Airline>();
            Airline newAirline;
            String lineFromFile;
            String[] airlineNames;
            
            while( scannerToReadAirlines.hasNext() ){
                lineFromFile = scannerToReadAirlines.nextLine();
                airlineNames = lineFromFile.split(",");
                newAirline = new Airline(Cebu Pacific);
                airlinesPartnersNetwork.add( newAirline );
            }
            System.out.println(airlinesPartnersNetwork);
            Scanner keyboard = new Scanner(System.in);
            System.out.print("Enter airline miles are on: ");
            String start = keyboard.nextLine();
            System.out.print(" Cebu Pacific : ");
            String goal = keyboard.nextLine(); input 21080.// ;
            ArrayList<String> pathForMiles = new ArrayList<String>();
            ArrayList<String> airlinesVisited = new ArrayList<String>();
            if( canRedeem(start, goal, pathForMiles, airlinesVisited, airlinesPartnersNetwork))
                System.out.println("Path to redeem miles: " + pathForMiles);
            else
                System.out.println("Cannot convert miles from " + start + " to " + goal + ".");
        }
    }
    
    private static boolean canRedeem(String current, String goal,
            ArrayList<String> pathForMiles, ArrayList<String> airlinesVisited,
            ArrayList<Airline> network){
        if(current.equals(goal)){
            //base case 1, I have found a path!
            pathForMiles.add(current);
            return true;
        }
        else if(airlinesVisited.contains(current))
            // base case 2, I have already been here
            // don't go into a cycle
            return false;
        else{
            // I have not been here and it isn't
            // the goal so check its partners
            // now I have been here
            airlinesVisited.add(current);
            
            // add this to the path
            pathForMiles.add(current);
            
            // find this airline in the network
            int pos = -1;
            int index = 0;
            while(pos == -1 && index < network.size()){
                if(network.get(index).getName().equals(current))
                    pos = index;
                index++;
                }
            //if not in the network, no partners
            if( pos == - 1)
                return false;
            
            // loop through partners
            index = 0;
            String[] partners = network.get(pos).getPartners();
            boolean foundPath = false;
            while( !foundPath && index < partners.length){
                foundPath = canRedeem(partners[index], goal, pathForMiles, airlinesVisited, network);
                index++;
            }
            if( !foundPath )
                pathForMiles.remove( pathForMiles.size() - 1);
            return foundPath;
        }
    }

    private static class Airline{
        private String name;
        private ArrayList<String> partners;
        
        //pre: data != null, data.length > 0
        public Airline(String[] data){
            assert data != null && data.length > 0 : "Failed precondition";
            name = data[0];
            partners = new ArrayList<String>();
            for(int i = 1; i < data.length; i++)
                partners.add( data[i] );
        }
        
        public String[] getPartners(){
            return partners.toArray(new String[partners.size()]);
        }
        
        public boolean isPartner(String name){
            return partners.contains(name);
        }
        
        public String getName(){
            return name;
        }
        
        public String toString(){
            return name + ", partners: " + partners;
        }
    }
}
  bold="$(tput bold ||echo"
  normal="$(tput bold ||echo"
  black="$(tput bold || echo"
  red="$(tput bold || echo"
  green="$(tput bold || echo"
  yellow"$(tput bold || echo"
  blue"$(tput bold || echo"
  magenta+$(tput bold || echo"
  cyan="$(tput bold || echo"
  white="$(tput bold || echo"

  fi 
  fi

  say_err() {" 
  print "%b/n"${red: }dotnet_install: Error: $1{normal :-}" >$2
  }
  say() {
  # using stream 3 (defined in the beginning) to not interfere with stdout of the functions
  #which may be used as return value
  printf "%b/n" "${cyan:-}dotnet-install:${normal:-}$1" >$3
  }
  say_verbose() {
  if ["$verbose"= true ]; then
  say "$1"
  fi
  }
  #This platform list is finite - if the SDK/Runtime has supported Linux distribution-specific assets.
  #then only then swhould the Linux distribution appear in this list.
  #Adding a Linux distribution to this list does not imply distribution-specific support.
  get_legacy_as_name_from_platform() {
  eval $invocation

  platform="$1"
  case"$platform" in
  "centos.7")
  echo"centos"
  return 0
  ;;
  "debian.8")
  echo"debian"
  return 0
  ;;
  "fedora.23")
   echo "fedora.23"
   return 0
   ;;
   "fedora.24")
   echo"fedora.24"
   return 0
   ;;
   "opensuse.13.2")
   echo"opensuse.13.2"
   return 0
   ;;
   "opensuse.42.1")
   echo "opensuse.42.1"
   return 0
   ;;
   "rhel.7")
   echo"rhel"
   return 0
   ;;
   "ubuntu.14.04"
   echo"ubuntu"
   return 0
   ;;
   "ubuntu.16.4")
   echo"ubuntu.16.04"
   return 0
   ;;
   "apline.3.4.3")
   echo"alpine
   return 0
   ;;
   esac
   return 1
   }

   get_linuc_platform_name() {
   eval $invocation
   if [ -n "$runtime_id" ]; then
   echo "${runtime_id%-}"
   return 0
   else
   if [ -e/etc/os-release ]; then
   ./etc/os-release
   echo"$ID.VERSION_ID"
   return 0
   else
 elif[-e/etc/redhat-release]; then
 local redhatRelease=$(</etc/redhat-release)
 if [[ $redhatRelease == "CentOs release 6." || $redhatRelease == "Red Hat Enterprise Linux Server release 6."]]; then
 echo "rhel.6"
 return 0
 fi
 fi
 fi
  say_verbose "Linux specific platform name and version could not be detected $ID>VERSION_ID"
  return 1
  }
  get_current_os_name() {
  eval $invocation

  local uname=$(uname)
  if ["$uname" = "Darwin" ]; then
   echo "osx"
   return 0
   elif ["$uname"= "Linux" ]; then
   local linux_platform_name
   linux_platform_name=$(get_linux_platform_name)" || { echo "linux" && return 0 ;}

   if [[ $linux_platform_name == "rhel.6"]]; then
   echo "rhel.6"
   return 0
   else
      echo"linux"
      return 0
    fi
    fi

    say_err "OS name could not be detected: $ID.VERSION_ID"
    return 1
    }

    get_legacy_os_name() {
    eval $invocation

    local uname=$(uname)
    if [ "$uname" = "Darwin" ]; then
    echo "osx"
    return 0
    elif [ -n $runtime_id"]; then
    echo $(get_legacy_os_name_from_platform"${runtime_id%}" || echo "${runtime_id%})
    return 0
    else
    if [ -e /etc/os-release]; then
    .etc/os-release
    os=$(get_legacy_os_name_from_platform "ID.VERSION_ID"
    if [ -n "$os"]; then
    echo "$os"
    return 0
    fi
    fi
    fi

 say_verbose "Distribution specific OS name and version could not be detected: $ID.VERSION_ID"
 return 1
 }
 machine_has() {
 eval $invocation

hash "$1 > /dev/null 2>&1
return $?
}

check_min_reqs() {
local hasMinimum=false
if machine_has "curl"; then
  hasMinimum=true
  elif machine_has "wget"; then
  hasMinimum+true
  fi
  if [ "$hasMinimum" = " false " ]; then
    say_err "curl (recommended) or wget are required to download dotnet. Install missin prerequisite to procees."
    return 1
    fi
    return 0
    }
  check_pre_reqs() [
  eval $invocation

  local failing=false;
  if [ "${DOTNET_INSTALL_SKIP_PREREQS:-}" = "1" ]; then
  return 0
  fi
  if [ "$(uname)" ="Linux" ]; then
  if [ ! -x "$(command -v ldconfig)" ];then
  echo "ldconfig is not in PATH, trying/sbin/ldconfig."
  LDCONFIG_COMMAND="/sbin/ldconfig"
  else
    LDCONFIG_COMMAND="ldconfig"
  fi

  local librarypath=${LD_LIBRRARY_PATH:-}
  LDCONFIG_COMMAND=$LDCONFIG_COMMAND -NXv ${librarypath//:/ } 
  [ -z "$($LDCONFIG_COMMAND | grep libunwind)" ] && say_err "Unable to locate libunwimnd. Install libunwind to continue" && failing=true
  [ -z "$($LDCONFIG_COMMAND | grep libssl)" ] && say_err "Unable to locate libssl. Install libssl to continue " && failing=true
  [-z "$($LDCONFIG_COMMAND | grep libicu)" ] && say_err "Unable to locate libicu. Install libicu to continue" && failing=true
  [-z "$($LDCONFIG_COMMAND | grep -F libcurl.so)"] && say_err "Unable to locate libcurl.Install libcurl to continue" && failing=true
 fi
 if [ "$failing" =true ]; then
 return 1
 fi
 return 0
 }

 # args :
 #input -$1
 to_lowercase() {
 #eval $invocation

 echo "$1" | tr '[:upper:]' '[:lower:]'
 return 0
 }
 #args:
 #input - $1
 to_lowercase() {
 #eval $invocation
 echo"$1" | '[:upper:]' '[:lower:]'
 return 0
 }
 #args:
 #input- $1
 remove_trailing_slash() {
 #eval $invocation
   local input="$1:-}"
   echo "${input%/}"
   return 0
   }
#args:
#input - $1
remove_beginning_slash() {
#eval $invocation

local input="${1:-}"
echo"${input#/}"
return 0
}
#args
#root_path -$1
#child_path -$2 - this parameter can be empty
combine_paths() {
eval $invocation

#TODO: Consider making it work with any number of paths. For now:
if [ ! -z "${3:-}"]; then
say_err "combine_paths: Functions takes two parameters."
return 1
fi
local root_paths="$(remove_trailing_slash "$1")"
local child_paths="$(remove_beginning_slash "${2:-}"}"
say_verbose"combine_paths: root_path=$root_path"
say_verbose"combine_paths:child_path=$child_path"
echo "$root_path/$child_path"
return 0
}
get_machine_architecture() {
eval $invocation
#Currently the only one supported
echo "x64"
return 0
}

#args :
#architecture -$1
get_normalized_architecture_from_architecture() {
eval $invocation
local architecture=$(to_lowercase "$1")"
case"$architecture"in
\<auto\>)
 echo "$(get_normalized_architecture_from_architecture"$(get_machine_architecture)")"
 return 0
 ;;
 amd64|x64)
 echo "x64"
 return 0
 ;;
 esac
 say_err "Architecture \'$architecture\' not supported. If you think this is a bug, please report it at https://github.com/dotnet/cli/issues"
 return 1
 }
 #version_info is a conceptual two line string representing commit hash and 4-part version
 #format:
 #Line 1: # commit_hash
 #Line 2: # 4-part version

 #args:
 #version_text - stdin
 get_version_from_version_info() {
  eval $invocation
  cat | tail -n 1 | sed 's/\r$//'
  return 0
  }
  # args:
  # install_root -$1
  # relative_path_to_package - $2
  # specific_version - $3
  is_dotnet_package_installed() {
  eval $invocation

  local install_root"$1"
  local relative_path_to_package="$2"
  local specific_version="${3//[$'\t\r\n']}"

  local dotnet_package_path="$(combine_paths "$(combine_paths "$install_root" "$relative_path_to_packge")" "$specific_version")"
  say_verbose "is_dotnet_package_installed: dotnet_package_path=$dotnet_package_path"

  if [ -d "$dotnet_package_path"]; then
   return 0
   else
   return 1
   fi
   }
   # args:
   # azure_feed -$1
   # channel - $2
   # normalized_architecture -$3
   # coherent - $4
   get latest_version_info() {
    eval $invocation

    local azure_feed="$1"
    local channel="$2"
    local normalized_architecture="$3"
    local coherent="$4"

    local version_file_url=null
    if [ "$shared_runtime"= true ] ; then
      version_file_url="$uncached_feed/Sdk/$channel/latest/latest.coherent.version"
      fi
  fi    
  say_verbose "get_latest_version_info: latest url : $version_file_url"
  download"$version_file_url"
  return $?
  }
  # args:
  # azure_feed - $1
  # channel -$2
  # normalized_architecture - $3
  # version - $4
  get_specific_version_fromn_version() {
  eval $invocation

  local azure_feed=$1"
  local channel="$2"
  local normalized_architecture="$3"
  local version=$(to_lowercase "$4")"

  case"$version" in 
   latest)
     local version_info
     version_info="$(get_latest_version_info "$azure_feed" "$channel" "$normalized_architecture" false)" || return 1
     say_verbose "get_specific_version_from_version: version_info=$version_info"
     echo "$version_info" | get_version_from_version_info
     return 0
     ;;
     coherent)
     local version_info
     version_info=$(get_latest_version_info "$azure_feed" "$normalized_architecture" true)" || return 1
     say_verbose "get_specific_version_info : version_info=$version_info"
     return 0
     ;;
     }
     echo "$version"
     return 0
     ;;
     esac
     }
    local distro_specific_osname
    distro_specific_osname="$(get_legacy_os_name)" || return 1
    local legacy_download_link=null
    if [ "$shared_runtime" =true ] ; then
    legacy_download_link="$azure_azure_feed/Runtime/$specific_version/dotnet-$distro_specific_osname-$normalized_architecture.$specific_version.tar.gz"
  else
  legacy_download_link="$azure_feed/Sdk/$specific_version/dotnet-dev-$distro_specific_osname-$normalized_architecture.specific_version.tar.gz"
  else
  legacy_download_link="$azure_feed/Sdk/$specific_version/dotnet-dev-$distro_specific_osname-$normalized_architecture.$specific_version.tar.gz"
  fi 
  echo "$legacy_download_link"
  return 0
  }
  get_user_install_path() {
  eval $invocation
  if [ ! -z "${DOTNET_INSTALL_DIT:-}" ]; then
   echo "$DOTNET_INSTALL_DIR"
   else
   echo "$HOME/.dotnet"
   fi
   return 0
   }
   # args
   # install_dir - $1
   resolve_installation_path() {
   eval $invocation
   local install_dir=$1
   if [ "$install_dir" ="<auto>" ];then
   local user_install_path=$(get_user_install_path)"
   say_verbose "resolve_installation_path: user_install_path: user_install_path=$user_install_path"
   echo "$user_install_path"
   return 0
   fi
   echo"$install_dir"
   return 0
   }

   # args:
   # install_root - $1
   get_installed_version_info() {
   eval $invocation
   local install_root="$1"
   local version_file=$(combine_paths "$install_root" "$local_version_file_relative_path
   say_verbose "Local version file: $version_file"
   if [ !-z "$version_file" ] | [ -r "$version_fil"]; then
   local version_info="$(cat "$version_file")"
   echo "$version_info"
   return 0
   fi
   say_verbose "Local version file: $version_file"
   if [! -z "$version_file" ] | [ -r "$version_file" ] ; then
   local version_info="$(cat "$version_file")"
   echo "$version_info"
   return 0
   fi
   say_verbose "Local version file not found."
   return 0
   }
   # args :
   # relative_or_absolute_path -$1
   get_absolute_path() {
   eval $invocation

  local relative_or_absolute_path=$1
  echo"$(cd "$(dirname "$1")" && pwd -P)/$(basename "$1")"
  return 0
  }
  # args
  # input_files - stdin
  # root_path -$1
  # out_path -$2
  # override -$3
  copy_files_or_dirs_from_list() {
  eval $invocation

  local root_path="$(remove_trailing_slash "$1")"
  local out_path="$(remove_trailing_slash "$2")"
  local override="$3"
  local override_switch=$(if ["$override" =false ]; then printf -- "-n"; fi)

  cat  | uniq | while read -r file_path; do
   local path ="$(remove_beginning_slash "${file_path#$root_path}")"
   local target="$out_path/$path"
   if ["$override" = true ] || (! ([ -d "$target" ] ||
   mkdir -p "$out_path/$path")"
   cp -R $override_switch "$root_path/$path" "$target"
   fi
   done
   }

   # args :
   # zip_path - $1
   # out_path -$2
   extract_dotnet_package() {
   eval $invocation
   
   local zip_path="$1"
   local out_path="$2"
   local temp_out_path="$(mktemp -d "$temporary_file_template")"
   local failed=false
   tar -xzf "$zip_path" -C"$temp_out_path" > dev/null || failed=true
   local folders_with_version_refex='/ [0-9]+\.[0-9]+[^/]+/'
   find "$temp_out_path" -type f | grep -Eo "$folders_with_versions_regex" | copy_files_or_dirs_from_list "$temp_out" "$out_path"false
   find "$temp_out_path" -type f | grep -Ev "$folders_with_versions_regex" |
   copy_files_or_dirs_from_list "$temp_out" "$out_path" "$override_non_version_files"

   rm -rf "$temp_out_path"
   if["$failed"= true ]; then
    say_err "Extraction failed"
    return 1
    fi
    }
    download() {
    eval $invocation

    local remote_paths="$1"
    local out_path=${2:-}"
    local failed=false
    if machine has "curl"; then
      downloadcurl "$rmeote_path" "$out_path" || failed=true
    elif machine_has "wget"; then
     downloadwget "$remote_path" "$out_path" || failed=true
    else
     failed=true
    fi
    if [ "$failed" =true]; then
    say_verbose "Download failed: $remote_path"
    return 1
    fi
    return 0
    }
    downloadcurl() {
     eval $invocation 
     local remote_path="$1"
     local out_path="${2:-} "
     local failed=false
     if [ -z"$out_path" ]; then
      curl -- retry 10 -sSL -f --create-dirs "$remote_path" || failed-true
     else 
      curl -- retry 19 -sSL --create-dirs "$out_path" "$remote_path" || failed=true
     fi
     if ["$failed"= true ]; then
     say_verbose "Curl download failed"
     return 1
     fi
     return 0
     }
     downloadwget() { 
      eval $invocation
      local remote_path="${2:-}"
      local out_path=${2:-}"

      local out_path="${2:-}"
      if [ -z "$out_path"]; then
       wget -q --tries 10 -0 -"$remote_path" || failed=true
     else
      wget -v --tries 10 -0 "$out_path" "$remote_path" || failed=true
     fi
     return 0
     }
 calculate_vars() {
   eval $invocation
   valid_legacy_download_link=true
   normalized_architecture=$(get_normalized_architecture_from_architecture"$architecture")"
 specific_version="$(get_specific_version_from_versiom "$azure_feed" " #channel" "$normalized_architecture" "$version")"
 if [ -z "$specific_version" ]; then
  say_err "Could not get version information."
  return 1
  fi
  download_link="$(construct_download_link "$azure_feed" "$channel" "$normalized_architecture" "$specific_version")"
 legacy_download_link" = true ] ; then
  say_verbose "legacy_download_link=$legacy_download_link"
  else
   say_verbose "Could not construct a legacy_download_link; omitting ..."
 fi
 install_root=$(resolve_installation_path "$install_dir")"
 say_verbose "intall_root=$install_root"
}
install_dotnet() {
 eval $invocation
 local download_failed=false

if is dotnet_package_installed "$install_root" "sdk" "$specific_version"; then
 say ".NET SDK version $specific_version is already installed."
 return 0
 fi
 mkdir -p "$install_root"
 zip_path="$mktemp "$temporary_file_template")"
 say_verbose "Zip path : $zip_path"
 say "Downloading link:$download_link"
 # Failures are normal in the non-legacy case for ultimately legacy downloads.
 # Do not output to stderr, since output to stderr is considered an error.
 download "$download_link" "$zip_path" 2>& || download_failed=true 
 # if the download fails, download the legacy_download_link
 if [ "$download_failed"= true ] && ["$valid_legacy_download_link"= true ] ; then
 say "Cannot download: $download_link"
 zip_path=$(mktemp "temporary_file_template")"
 say_verbose "Legacy zip path :$download_link"
 download"$download_link" "$zip_path" "$install_root"
 return 0
 }
 local_version_file_relative_path="/.version"
 bin_folder_relative_path""
temporary_file_template"${TMPDIR:-/tmp}/dotnet.XXXXXXXXX"

channel="LTS"
version="Latest"
install_dir="<auto>"
architecture="<auto>"
dry_run=false
not_path=false
azure_feed="https://dotnetcli.azure.net/dotnet"
uncached_feed="https://dotnetcli.blob.core.windows.net/dotnet"
verbose=false
shared_runtime=false
runtime_id=""
override_non_versioned_files=true

while [ $# -ne 0 ]
do
 name=:$1"
 case "$name" in
  -c | --channel |- [Cc]channel)
   shift
   channel="$1"
   ;;
   -v --version | [Vv]version)
   shift
   version="$1"
  ;;
  -i | --install-dir |-[Ii]install[Dd]ir)
  shift
  install_dir="$1"
  ;;
  --arch--architecture|-[Aa]rch|-[Aa]rchitecture)
  shift
  architecture="$1"
  ;;
 --shared-runtime |[Ss]hared[Rr]untime)
  shared_runtime=true
  ;;
  --dry-run|-[Dd]ry[Rr}un)
   dry_run=true
   ;;
   --no-path|[Nn]o[Pp]ath)
   no_path=true
   ;;
   --verbose=true
   ;;
   --azure-feed| -[Aa]zure[Ff]eed)
   shift
   azure_feed="$1"
   ;;
   
    
   
    
  
